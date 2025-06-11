Great! Here's how to set up a complete Spring Boot application using:

✅ Entity, DTO

✅ Repository

✅ Service

✅ Controller

✅ MapStruct for mapping



---

🏗️ Use Case: Manage Projects and Team Members (with nested Role mapping)


---

📁 Project Structure (Package Suggestions)

com.example.projectmapstruct
├── controller
│   └── ProjectController.java
├── dto
│   ├── ProjectDTO.java
│   └── TeamMemberDTO.java
├── entity
│   ├── ProjectEntity.java
│   ├── RoleEntity.java
│   └── TeamMemberEntity.java
├── mapper
│   └── ProjectMapper.java
├── repository
│   ├── ProjectRepository.java
│   └── TeamMemberRepository.java
├── service
│   ├── ProjectService.java
│   └── ProjectServiceImpl.java
└── ProjectMapstructApplication.java


---

✅ 1. Entity Classes (entity package)

RoleEntity.java

@Entity
public class RoleEntity {
    @Id
    private String code;
    private String name;

    // Constructors, Getters, Setters
}

TeamMemberEntity.java

@Entity
public class TeamMemberEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String fullName;

    @ManyToOne(cascade = CascadeType.ALL)
    private RoleEntity role;

    @ManyToOne
    private ProjectEntity project;

    // Getters, Setters
}

ProjectEntity.java

@Entity
public class ProjectEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String projectName;

    @OneToMany(mappedBy = "project", cascade = CascadeType.ALL)
    private List<TeamMemberEntity> team;

    // Getters, Setters
}


---

✅ 2. DTOs (dto package)

TeamMemberDTO.java

public class TeamMemberDTO {
    private Long id;
    private String fullName;
    private String role;
}

ProjectDTO.java

public class ProjectDTO {
    private Long id;
    private String name;
    private List<TeamMemberDTO> members;
}


---

✅ 3. MapStruct Mapper (mapper package)

ProjectMapper.java

@Mapper(componentModel = "spring")
public interface ProjectMapper {
    @Mapping(source = "projectName", target = "name")
    @Mapping(source = "team", target = "members")
    ProjectDTO toDto(ProjectEntity entity);

    @Mapping(source = "name", target = "projectName")
    @Mapping(source = "members", target = "team")
    ProjectEntity toEntity(ProjectDTO dto);

    @Mapping(source = "role.name", target = "role")
    TeamMemberDTO toDto(TeamMemberEntity entity);

    @Mapping(source = "role", target = "role", qualifiedByName = "mapRoleName")
    TeamMemberEntity toEntity(TeamMemberDTO dto);

    @Named("mapRoleName")
    default RoleEntity mapRole(String roleName) {
        switch (roleName.toLowerCase()) {
            case "developer": return new RoleEntity("DEV", "Developer");
            case "qa": return new RoleEntity("QA", "QA Engineer");
            default: return new RoleEntity("UNK", roleName);
        }
    }
}


---

✅ 4. Repositories (repository package)

ProjectRepository.java

public interface ProjectRepository extends JpaRepository<ProjectEntity, Long> {}

TeamMemberRepository.java

public interface TeamMemberRepository extends JpaRepository<TeamMemberEntity, Long> {}


---

✅ 5. Service Layer (service package)

ProjectService.java

public interface ProjectService {
    ProjectDTO saveProject(ProjectDTO dto);
    List<ProjectDTO> getAllProjects();
}

ProjectServiceImpl.java

@Service
public class ProjectServiceImpl implements ProjectService {

    @Autowired
    private ProjectRepository projectRepository;

    @Autowired
    private ProjectMapper mapper;

    @Override
    public ProjectDTO saveProject(ProjectDTO dto) {
        ProjectEntity entity = mapper.toEntity(dto);
        entity.getTeam().forEach(member -> member.setProject(entity)); // set reverse ref
        return mapper.toDto(projectRepository.save(entity));
    }

    @Override
    public List<ProjectDTO> getAllProjects() {
        return projectRepository.findAll().stream()
                .map(mapper::toDto)
                .collect(Collectors.toList());
    }
}


---

✅ 6. Controller (controller package)

ProjectController.java

@RestController
@RequestMapping("/api/projects")
public class ProjectController {

    @Autowired
    private ProjectService projectService;

    @PostMapping
    public ResponseEntity<ProjectDTO> saveProject(@RequestBody ProjectDTO dto) {
        return ResponseEntity.ok(projectService.saveProject(dto));
    }

    @GetMapping
    public ResponseEntity<List<ProjectDTO>> getAllProjects() {
        return ResponseEntity.ok(projectService.getAllProjects());
    }
}


---

✅ 7. Main Class

@SpringBootApplication
public class ProjectMapstructApplication {
    public static void main(String[] args) {
        SpringApplication.run(ProjectMapstructApplication.class, args);
    }
}


---

✅ 8. Sample JSON for POST /api/projects

{
  "name": "AI Assistant",
  "members": [
    {
      "fullName": "Ankur Gautam",
      "role": "Developer"
    },
    {
      "fullName": "Riya Sharma",
      "role": "QA"
    }
  ]
}


---

🧾 Dependencies (Maven)

<dependency>
    <groupId>org.mapstruct</groupId>
    <artifactId>mapstruct</artifactId>
    <version>1.5.5.Final</version>
</dependency>
<dependency>
    <groupId>org.mapstruct</groupId>
    <artifactId>mapstruct-processor</artifactId>
    <version>1.5.5.Final</version>
    <scope>provided</scope>
</dependency>

> ✅ Use lombok optionally to reduce boilerplate
✅ Enable annotation processing in your IDE (important for MapStruct)




---

Would you like:

A full working ZIP file (you can import to IntelliJ or VS Code)?

This in Gradle version?

Add tests using JUnit?


Let me know!

