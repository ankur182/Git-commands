Hi, I’m Ankur Gautam, currently pursuing my B.Tech in Computer Science from DTU.
During college, I focused a lot on Data Structures and Algorithms, and also explored frontend development by building projects like a Zoom clone, a restaurant website, and a fitness app.

Since stepping into the corporate environment, my interest has shifted more towards backend development, and I’m currently deepening my understanding of Java and Spring Boot.

Outside of work, I’ve recently picked up gymming, which has helped me maintain a healthy routine — though it's tough to always eat clean in a city like Mumbai! I also enjoy playing sports with my colleagues.
I’m always eager to learn, take ownership, and grow both technically and personally.

--------------------------------------

🔹 Agenda Breakdown & What to Expect
1. Objectives for Hiring Grads
What they may say:

Why grads are hired.

What value fresh minds bring.

Vision for your learning curve and growth.

Smart way to respond:

Emphasize your adaptability, eagerness to learn, and fresh perspective.

Mention you’re keen to contribute actively and grow alongside the team.

💬 “I believe grads bring fresh energy and can adapt quickly. I’m eager to understand business-level impact and contribute meaningfully, not just code-wise but also by picking up responsibilities that support the team’s goals.”

2. Expectations from Individuals Post Joining
What they may expect from you:

Proactiveness in learning.

Willingness to take ownership.

Ask questions, but also try to understand the context before asking.

Keep up with deliverables, even while learning.

Smart way to show readiness:

Mention your ability to take initiative, work through blockers independently when possible, and communicate clearly.

💬 “While I’m still learning, I’m someone who takes initiative and likes to understand things in depth. I aim to balance learning with delivery and ensure I’m dependable when it comes to deadlines and responsibilities.”

3. Collective Roles and Responsibilities
What this could mean:

Understanding team dynamics.

You’re not just an individual contributor — you're part of a unit.

Accountability, collaboration, and communication are key.

Smart points to highlight:

Show that you value team collaboration.

Mention how you’ve worked on team projects in the past.

Show willingness to take ownership while being a team player.

💬 “I strongly believe in team synergy — I’ve seen during college projects that when roles are clear and communication is open, outcomes are great. I look forward to collaborating, supporting others, and learning from experienced teammates.”

💡 Bonus Smart Add-ons You Can Use
“I'm particularly interested in understanding not just the 'how' but also the 'why' behind the systems we build.”

“I’m open to feedback and always looking to improve — I see this opportunity as a chance to build both my technical and professional mindset.”

“Time management and clear communication are two habits I’ve been working on since college, and I’d like to keep improving here.”






..



public Asset abandonOrRecoverAsset(String assetId, boolean abandon) throws AssetNotFoundException {
    String performedBy = authenticatedUser.getCurrentUser();
    Asset asset = findOrUpdateAssetByIdForWrite(assetId)
        .orElseThrow(() -> new AssetNotFoundException(assetId));

    AssetStatus previousAssetStatus = asset.getAssetStatus();
    TargetType targetType;
    ActionType actionType;

    if (abandon) {
        asset.setAssetStatus(AssetStatus.ABANDONED, Clock.now(), performedBy);
        targetType = TargetType.ABANDONED;
        actionType = ActionType.UPDATE;
    } else {
        asset.setAssetStatus(AssetStatus.RECOVERED, Clock.now(), performedBy);
        targetType = TargetType.RECOVERED;
        actionType = ActionType.UPDATE;
    }

    // ✅ Build EventDetail set
    Set<EventDetail> details = Set.of(
        EventDetail.builder()
            .eventDetailType(EventDetailType.ASSET_STATUS)
            .value(targetType.name())   // "ABANDONED" or "RECOVERED"
            .build()
    );

    // ✅ Save audit trail
    auditTrailPort.save(
        buildAuditTrail(asset, TargetType.ASSET_STATUS, actionType, details)
    );

    eventPublisher.publishEvents(modAsset);
    return asset;
}
