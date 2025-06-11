// ProjectEntity.java package com.example.myapp.entity;

import jakarta.persistence.*; import java.util.List;

@Entity public class ProjectEntity { @Id @GeneratedValue(strategy = GenerationType.IDENTITY) private Long id;

private String projectName;

@OneToMany(mappedBy = "project", cascade = CascadeType.ALL, orphanRemoval = true)
private List<TeamMemberEntity> team;

// Getters and setters

}

// TeamMemberEntity.java package com.example.myapp.entity;

import jakarta.persistence.*;

@Entity public class TeamMemberEntity { @Id @GeneratedValue(strategy = GenerationType.IDENTITY) private Long id;

private String name;

@ManyToOne
private RoleEntity role;

@ManyToOne
private ProjectEntity project;

// Getters and setters

}

// RoleEntity.java package com.example.myapp.entity;

import jakarta.persistence.*;

@Entity public class RoleEntity { @Id private String code; private String name;

public RoleEntity() {}

public RoleEntity(String code, String name) {
    this.code = code;
    this.name = name;
}

// Getters and setters

}

// ProjectDTO.java package com.example.myapp.dto;

import java.util.List;

public class ProjectDTO { private String name; private List<TeamMemberDTO> members;

// Getters and setters

}

// TeamMemberDTO.java package com.example.myapp.dto;

public class TeamMemberDTO { private String name; private String role;

// Getters and setters

}

// ProjectRepository.java package com.example.myapp.repository;

import com.example.myapp.entity.ProjectEntity; import org.springframework.data.jpa.repository.JpaRepository;

public interface ProjectRepository extends JpaRepository<ProjectEntity, Long> {}

// TeamMemberRepository.java package com.example.myapp.repository;

import com.example.myapp.entity.TeamMemberEntity; import org.springframework.data.jpa.repository.JpaRepository;

public interface TeamMemberRepository extends JpaRepository<TeamMemberEntity, Long> {}

// ProjectMapper.java package com.example.myapp.mapper;

import com.example.myapp.dto.; import com.example.myapp.entity.; import org.mapstruct.*; import java.util.List;

@Mapper(componentModel = "spring") public interface ProjectMapper { @Mapping(source = "projectName", target = "name") @Mapping(source = "team", target = "members") ProjectDTO toDto(ProjectEntity entity);

@Mapping(source = "name", target = "projectName")
@Mapping(source = "members", target = "team")
ProjectEntity toEntity(ProjectDTO dto);

@Mapping(source = "role.name", target = "role")
TeamMemberDTO toDto(TeamMemberEntity entity);

@Mapping(source = "role", target = "role", qualifiedByName = "mapRole")
TeamMemberEntity toEntity(TeamMemberDTO dto);

@Named("mapRole")
default RoleEntity mapRole(String name) {
    return switch (name.toLowerCase()) {
        case "developer" -> new RoleEntity("DEV", "Developer");
        case "qa" -> new RoleEntity("QA", "QA Engineer");
        default -> new RoleEntity("UNK", name);
    };
}

}

// ProjectService.java package com.example.myapp.service;

import com.example.myapp.dto.ProjectDTO; import java.util.List;

public interface ProjectService { ProjectDTO saveProject(ProjectDTO dto); List<ProjectDTO> getAllProjects(); }

// ProjectServiceImpl.java package com.example.myapp.service;

import com.example.myapp.dto.ProjectDTO; import com.example.myapp.entity.ProjectEntity; import com.example.myapp.mapper.ProjectMapper; import com.example.myapp.repository.ProjectRepository; import org.springframework.beans.factory.annotation.Autowired; import org.springframework.stereotype.Service;

import java.util.List; import java.util.stream.Collectors;

@Service public class ProjectServiceImpl implements ProjectService {

@Autowired
private ProjectRepository projectRepository;

@Autowired
private ProjectMapper mapper;

@Override
public ProjectDTO saveProject(ProjectDTO dto) {
    ProjectEntity entity = mapper.toEntity(dto);
    entity.getTeam().forEach(member -> member.setProject(entity));
    return mapper.toDto(projectRepository.save(entity));
}

@Override
public List<ProjectDTO> getAllProjects() {
    return projectRepository.findAll().stream()
            .map(mapper::toDto)
            .collect(Collectors.toList());
}

}

// ProjectController.java package com.example.myapp.controller;

import com.example.myapp.dto.ProjectDTO; import com.example.myapp.service.ProjectService; import org.springframework.beans.factory.annotation.Autowired; import org.springframework.http.ResponseEntity; import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController @RequestMapping("/api/projects") public class ProjectController {

@Autowired
private ProjectService projectService;

@PostMapping
public ResponseEntity<ProjectDTO> save(@RequestBody ProjectDTO dto) {
    return ResponseEntity.ok(projectService.saveProject(dto));
}

@GetMapping
public ResponseEntity<List<ProjectDTO>> getAll() {
    return ResponseEntity.ok(projectService.getAllProjects());
}

}
