private void LoadEmailMatrix()
{
    Logger.LogInformation("LoadEmailMatrixExcelData - start");

    var filePath = EmailMatrixConstants.ExcelTemplatePath;
    if (!File.Exists(filePath))
        throw new FileNotFoundException($"Excel file is missing: {filePath}");

    using var package = new ExcelPackage(new FileInfo(filePath));
    var worksheet = package.Workbook.Worksheets[EmailMatrixConstants.WorksheetName];

    var siteNames = ExcelHelper.ReadRowStrings(worksheet, EmailMatrixConstants.SiteNameRangeName);
    var notifNames = ExcelHelper.ReadRowStrings(worksheet, EmailMatrixConstants.NotifNameRangeName);

    Logger.LogInformation("LoadEmailMatrixExcelData - headers read");

    CheckValidNames(siteNames, notifNames);

    var matrixRange = worksheet.Names[EmailMatrixConstants.MatrixRangeName].Offset(1, 0);
    var notifEmailList = new List<EmailMatrixNotificationDTO>();

    for (int siteIndex = 0; siteIndex < siteNames.Count; siteIndex++)
    {
        for (int notifIndex = 0; notifIndex < notifNames.Count; notifIndex++)
        {
            var email = matrixRange.GetValue(siteIndex, notifIndex)?.ToString().Trim();

            if (!RegexHelper.IsValidMailObject(email))
                throw new ArgumentException($"Invalid email: {email}");

            notifEmailList.Add(new EmailMatrixNotificationDTO
            {
                SITENAME = siteNames[siteIndex],
                NOTIFICATIONTYPEID = notifNames[notifIndex],
                EMAILADDRESS = email
            });
        }
    }

    _emailMatrixRepo.SaveEmailMatrix(notifEmailList);
    Logger.LogInformation("LoadEmailMatrixExcelData - completed");
}

private void CheckValidNames(List<string> siteNames, List<string> notifNames)
{
    var validSites = _siteRepo.GetAllSites();
    var validNotifs = _notifRepo.GetAllNotificationTypes();

    var invalidSites = siteNames.Except(validSites).ToList();
    if (invalidSites.Any())
        throw new ArgumentException("Invalid site names: " + string.Join(", ", invalidSites));

    var invalidNotifs = notifNames.Except(validNotifs).ToList();
    if (invalidNotifs.Any())
        throw new ArgumentException("Invalid notification types: " + string.Join(", ", invalidNotifs));
}
