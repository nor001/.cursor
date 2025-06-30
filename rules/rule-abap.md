# ABAP RULES (SAP Corporate Compatible)

> Todas las reglas ABAP (development, corporate, legacy, RAP, performance) deben estar en este único archivo plano por restricciones SAP.

---

## 1. DEVELOPMENT

### ABAP Environment Constraints
- NO `.cursor/` folders allowed in SAP project directories
- Corporate restrictions on file system modifications
- SSL/Proxy requirements for external connections
- Legacy system compatibility requirements
- Strict naming conventions and coding standards

### Naming Conventions
- Usar prefijos corporativos (ej: ZCL_, YCL_)
- Nombres descriptivos y en inglés

### Standard Patterns
```abap
CLASS zcl_my_service DEFINITION PUBLIC FINAL CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_rap_query_provider.
    INTERFACES if_rap_command_handler.
    INTERFACES if_rap_update_handler.
ENDCLASS.
```

---

## 2. CORPORATE

### File System Restrictions
- NO carpetas ni subcarpetas
- NO archivos temporales fuera de /tmp
- Cumplir con políticas de seguridad corporativa

### Security Patterns
```abap
IF NOT is_authorized( user ).
  MESSAGE e001(zmsg) WITH 'No authorization'.
  RETURN.
ENDIF.
```

---

## 3. LEGACY

### Compatibility
- Mantener compatibilidad con versiones antiguas de SAP
- Usar solo funciones estándar

### Migration Pattern
```abap
IF is_legacy_system( ).
  PERFORM legacy_process USING data.
ELSE.
  PERFORM modern_process USING data.
ENDIF.
```

---

## 4. RAP (RESTful ABAP Programming)

### RAP Patterns
```abap
CLASS zbp_my_rap_handler DEFINITION INHERITING FROM cl_abap_behavior_handler.
  PUBLIC SECTION.
    METHODS get_entity FOR READ BY KEY.
ENDCLASS.
```

---

## 5. PERFORMANCE

### Performance Optimization
- Usar buffering donde sea posible
- Evitar SELECT dentro de loops

### Example
```abap
SELECT * FROM ztable INTO TABLE @DATA(result) WHERE status = @status.
LOOP AT result INTO DATA(row).
  " Procesar row
ENDLOOP.
```

---

## 6. SPECIAL CASES
- Documentar cualquier lógica especial o workaround aquí.

---

## 7. TRIGGERS Y CONTEXTO

### ABAP Development Triggers
```bash
# ABAP-specific triggers (manual activation)
@abap-development    # Activa todas las reglas ABAP
@rap-development     # Activa reglas específicas de RAP
@abap-corporate      # Activa reglas de restricciones corporativas
@abap-legacy         # Activa reglas de compatibilidad legacy
```

### Performance & API Optimization Triggers
```bash
# Performance-specific triggers (automatic detection + manual activation)
@performance-audit   # Activa auditoría de performance completa
@api-optimization    # Activa optimización de llamadas API
@react-strict-mode   # Activa manejo específico de React Strict Mode
@legacy-migration    # Activa migración gradual de sistemas legacy
@debug-performance   # Activa componentes de debug de performance
@emergency-mode      # Activa protocolos de emergencia de performance
```

### ABAP vs Web Development Context
```typescript
// Context detection for different development environments
interface DevelopmentContext {
  environment: 'abap' | 'web' | 'hybrid';
  constraints: CorporateConstraints;
  rules: RuleSet;
}

function detectDevelopmentContext(): DevelopmentContext {
  // Detect ABAP environment
  if (isABAPProject()) {
    return {
      environment: 'abap',
      constraints: getABAPCorporateConstraints(),
      rules: getABAPRules()
    };
  }
  
  // Detect web environment
  if (isWebProject()) {
    return {
      environment: 'web',
      constraints: getWebConstraints(),
      rules: getWebRules()
    };
  }
  
  // Hybrid environment
  return {
    environment: 'hybrid',
    constraints: getHybridConstraints(),
    rules: getHybridRules()
  };
}
```

---

## 8. ENTORNOS CORPORATIVOS SAP

### Corporate Environment Constraints
- SSL/Proxy requirements for external connections
- Corporate restrictions on file system modifications
- Legacy system compatibility requirements
- Strict naming conventions and coding standards

### Special CSV Formats (SAP Export)
```abap
" Handling SAP CSV exports with headers on line 3
FUNCTION process_sap_csv_export.
  " Skip first 2 lines (SAP metadata)
  " Header on line 3
  " Data starts from line 4
  DATA: lv_line TYPE string,
        lv_line_number TYPE i.
  
  LOOP AT csv_lines INTO lv_line.
    lv_line_number = sy-tabix.
    
    IF lv_line_number <= 2.
      " Skip SAP metadata lines
      CONTINUE.
    ELSEIF lv_line_number = 3.
      " Process headers
      PERFORM process_headers USING lv_line.
    ELSE.
      " Process data
      PERFORM process_data_line USING lv_line.
    ENDIF.
  ENDLOOP.
ENDFUNCTION.
```

### Corporate Data Processing Patterns
```abap
" Standard pattern for corporate data validation
FUNCTION validate_corporate_data.
  " 1. Check corporate format compliance
  IF NOT is_corporate_format_compliant( data ).
    MESSAGE e002(zmsg) WITH 'Data does not comply with corporate format'.
    RETURN.
  ENDIF.
  
  " 2. Validate business rules
  IF NOT validate_business_rules( data ).
    MESSAGE e003(zmsg) WITH 'Business rule validation failed'.
    RETURN.
  ENDIF.
  
  " 3. Check security constraints
  IF NOT check_security_constraints( data ).
    MESSAGE e004(zmsg) WITH 'Security validation failed'.
    RETURN.
  ENDIF.
ENDFUNCTION.
```

---

## 9. INTEGRACIÓN WEB-SAP

### Hybrid Environment Handling
```abap
" When working with both web and SAP environments
FUNCTION handle_hybrid_data_exchange.
  " Convert web format to SAP format
  IF is_web_format( input_data ).
    DATA(sap_data) = convert_web_to_sap( input_data ).
  ENDIF.
  
  " Process with SAP business logic
  PERFORM sap_business_process USING sap_data.
  
  " Convert back to web format if needed
  IF output_format = 'WEB'.
    output_data = convert_sap_to_web( sap_data ).
  ENDIF.
ENDFUNCTION.
```

### Corporate CSV Format Standards
- Headers on line 3 (SAP standard export format)
- Metadata in first 2 lines (system info, export timestamp)
- UTF-8 encoding with BOM for compatibility
- Corporate field naming conventions
- Mandatory audit fields (created_by, created_at, etc.)

---

## 10. DEBUGGING SAP ENVIRONMENTS

### SAP-specific Debug Patterns
```abap
" Standard debugging approach for SAP systems
FUNCTION debug_sap_issue.
  " 1. Check system status
  CALL FUNCTION 'CHECK_SYSTEM_STATUS'
    IMPORTING
      system_ok = DATA(lv_system_ok).
  
  " 2. Validate authorizations
  AUTHORITY-CHECK OBJECT 'S_DEVELOP'
    ID 'DEVCLASS' FIELD '*'
    ID 'OBJTYPE' FIELD '*'
    ID 'OBJNAME' FIELD '*'
    ID 'P_GROUP' FIELD '*'.

  IF sy-subrc <> 0.
    MESSAGE e005(zmsg) WITH 'No authorization for debugging'.
    RETURN.
  ENDIF.
  
  " 3. Execute debug steps
  PERFORM debug_steps.
ENDFUNCTION.
```

### Environment Detection
```abap
" Detect current SAP environment type
FUNCTION detect_sap_environment.
  " Check if running in SAP system
  IF sy-sysid IS NOT INITIAL.
    " SAP system detected
    environment = 'SAP'.
    
    " Detect system type
    IF sy-sysid+0(1) = 'D'.
      system_type = 'DEVELOPMENT'.
    ELSEIF sy-sysid+0(1) = 'Q'.
      system_type = 'QUALITY'.
    ELSEIF sy-sysid+0(1) = 'P'.
      system_type = 'PRODUCTION'.
    ENDIF.
  ELSE.
    " Non-SAP environment
    environment = 'WEB'.
  ENDIF.
ENDFUNCTION.
```

---

## 11. CONFIGURACIÓN Y CONSTANTES SAP

### **Configuration & Constants Centralization (SAP)**
- **ALWAYS centralize configuration values** específicos de SAP (nombres de archivos, URLs, claves de API, etc.)
- **NEVER hardcode values** que aparecen en múltiples archivos SAP
- **ALWAYS create constants** para strings, números o configuraciones repetidas en proyectos SAP
- **ALWAYS validate consistency** en todos los archivos SAP usando los mismos valores
- **Document configuration patterns** y su uso en todo el sistema SAP

### **Configuración SAP/ABAP Específica**
```abap
" ALWAYS create centralized constants for SAP projects
CONSTANTS: BEGIN OF gc_sap_config,
             files TYPE string VALUE 'sap_project_data.csv',
             download TYPE string VALUE 'sap_project_data.csv',
             original TYPE string VALUE 'sap-projects.csv',
             assigned TYPE string VALUE 'sap-projects-assigned.csv',
           END OF gc_sap_config.

" ALWAYS include SAP-specific API endpoints
CONSTANTS: BEGIN OF gc_sap_endpoints,
             upload TYPE string VALUE '/api/upload',
             download TYPE string VALUE '/api/download-csv',
             sync TYPE string VALUE '/api/sync-to-supabase',
           END OF gc_sap_endpoints.
```

### **SAP Integration Constants**
```abap
" SAP environment detection constants
CONSTANTS: BEGIN OF gc_sap_environment,
             abap TYPE string VALUE 'ABAP',
             web TYPE string VALUE 'WEB', 
             hybrid TYPE string VALUE 'HYBRID',
           END OF gc_sap_environment.

" SAP layer configurations
CONSTANTS: BEGIN OF gc_sap_layers,
             special_care TYPE string VALUE 'ABAP_SPECIAL_CARE_LAYER',
             standard TYPE string VALUE 'OPERATIONAL_LAYER',
           END OF gc_sap_layers.
```

---

## 12. LAYER SYSTEM SAP

### **SAP-Specific Layer Selection**
```abap
FUNCTION select_sap_layer.
  " ABAP environment - always use special care
  IF context-environment = gc_sap_environment-abap.
    layer = gc_sap_layers-special_care.
    RETURN.
  ENDIF.
  
  " Performance issues detected - activate performance auditing layer
  IF context-performance_issues = 'CRITICAL'.
    layer = 'PERFORMANCE_AUDIT_LAYER'.
    RETURN.
  ENDIF.
  
  " Default SAP operational efficiency
  layer = gc_sap_layers-standard.
ENDFUNCTION.
```

### **SAP Manual Layer Override**
```abap
" SAP-specific explicit triggers:
" mode: abap = Force ABAP development mode with all constraints
" mode: sap-special-care = ABAP operational with extra attention to edge cases
```

---

## 13. OPERATING MODES SAP

### **🏢 ABAP-CARE (ABAP Development)**
```abap
" ABAP-CARE Mode Configuration
CONSTANTS: BEGIN OF gc_abap_care,
             " Triggers: ABAP project detected, corporate constraints, legacy systems
             trigger_project TYPE string VALUE 'ABAP_PROJECT_DETECTED',
             trigger_corporate TYPE string VALUE 'CORPORATE_CONSTRAINTS',
             trigger_legacy TYPE string VALUE 'LEGACY_SYSTEMS',
             
             " AI Integration: Conservative approach with ABAP-specific patterns
             ai_integration TYPE string VALUE 'CONSERVATIVE_ABAP_PATTERNS',
             
             " Security: Corporate security requirements + ABAP standards
             security TYPE string VALUE 'CORPORATE_ABAP_STANDARDS',
             
             " Special Cases: ABAP-specific business logic preservation
             special_cases TYPE string VALUE 'ABAP_BUSINESS_LOGIC',
             
             " Output: ABAP-compliant implementation with corporate constraints
             output TYPE string VALUE 'ABAP_COMPLIANT_IMPLEMENTATION',
           END OF gc_abap_care.
```

### **SAP Special Case Handling**
```abap
FUNCTION handle_sap_special_case.
  " 1. Identify SAP special case type
  case_type = identify_sap_special_case( data, context ).
  
  " 2. Apply appropriate SAP handler
  CASE case_type.
    WHEN 'format_variation'.
      result = handle_sap_format_variation( data ).
    WHEN 'corporate_constraint'.
      result = handle_sap_corporate_constraint( data ).
    WHEN 'business_rule'.
      result = handle_sap_business_rule( data ).
    WHEN 'abap_specific'.
      result = handle_abap_specific( data ).
    WHEN OTHERS.
      result = handle_sap_default_case( data ).
  ENDCASE.
ENDFUNCTION.

" ALWAYS include SAP detection logic
FUNCTION identify_sap_special_case.
  IF has_sap_format_variation( data ).
    case_type = 'format_variation'.
  ELSEIF has_sap_corporate_constraint( context ).
    case_type = 'corporate_constraint'.
  ELSEIF has_sap_business_rule( data ).
    case_type = 'business_rule'.
  ELSEIF is_abap_project( context ).
    case_type = 'abap_specific'.
  ELSE.
    case_type = 'default'.
  ENDIF.
ENDFUNCTION.
```

---

## 14. SAP RULE ACTIVATION SYSTEM

### **SAP Context Detection**
```abap
" ALWAYS detect SAP context and activate appropriate rules
TYPES: BEGIN OF ty_sap_context_detection,
         frontend TYPE abap_bool,
         backend TYPE abap_bool,
         database TYPE abap_bool,
         performance TYPE abap_bool,
         abap TYPE abap_bool,
       END OF ty_sap_context_detection.

FUNCTION detect_sap_context.
  context-frontend = check_sap_frontend_components( ).
  context-backend = check_sap_backend_components( ).
  context-database = check_sap_database_components( ).
  context-performance = check_sap_performance_issues( ).
  context-abap = check_abap_files( ) OR check_sap_project( ) OR check_corporate_constraints( ).
ENDFUNCTION.
```

### **SAP Rule Activation Triggers**
```abap
" SAP-specific triggers (manual activation)
" @abap-development    # Activa todas las reglas ABAP
" @rap-development     # Activa reglas específicas de RAP
" @abap-corporate      # Activa reglas de restricciones corporativas
" @abap-legacy         # Activa reglas de compatibilidad legacy
" @abap-detected       # Activates ABAP rules (dual activation)
" @abap-rules          # Force ABAP rules activation (dual)
```

### **SAP Rule Priority System**
```abap
" ALWAYS prioritize SAP rules based on context
" SUPPORT dual activation with SAP hierarchy
CONSTANTS: BEGIN OF gc_sap_rule_priority,
             critical TYPE string VALUE 'abap-rules,emergency-protocols',
             high TYPE string VALUE 'abap-rules,sap-corporate-rules',
             medium TYPE string VALUE 'sap-performance,sap-legacy',
             low TYPE string VALUE 'sap-documentation,sap-testing',
           END OF gc_sap_rule_priority.

FUNCTION activate_sap_rules.
  " 1. ALWAYS activate critical ABAP rules (base universal)
  activate_critical_abap_rules( ).
  
  " 2. Activate SAP context-specific rules (can override base rules)
  IF context-abap = abap_true.
    WRITE: 'ABAP context detected - activating ABAP rules (dual activation)'.
    activate_abap_rules( ). " Can override some general patterns
  ENDIF.
ENDFUNCTION.

FUNCTION activate_abap_rules.
  " ABAP rules can override general patterns for SAP-specific cases
  " Example: File system restrictions, naming conventions, corporate constraints
  WRITE: 'ABAP rules activated - may override general patterns'.
ENDFUNCTION.
```

### **SAP Rule Hierarchy System**
```abap
" RULE HIERARCHY: SAP-specific rules can override general rules
TYPES: BEGIN OF ty_sap_rule_hierarchy,
         base TYPE string,           " Always active (security, documentation, etc.)
         specific TYPE string,       " Can override base rules when needed
         domain TYPE string,         " SAP domain-specific patterns
       END OF ty_sap_rule_hierarchy.

" Example of SAP rule override:
FUNCTION handle_sap_file_operation.
  " Base rule (user-rules): Create files where needed
  IF operation-type = 'create'.
    " ABAP rule override: NO folders in SAP projects
    IF is_sap_project( ) AND operation-path CS '/'.
      MESSAGE e001(zsap) WITH 'ABAP rule: No folders allowed in SAP projects'.
      RETURN.
    ENDIF.
    
    " Base rule: Proceed with creation
    create_sap_file( operation-path ).
  ENDIF.
ENDFUNCTION.
```

### **SAP Activation Examples**
```abap
" When working on ABAP development
" @abap-detected
" Activates: user-rules + abap-rules (dual activation)

" When working on ABAP with performance issues  
" @abap-detected @performance-detected
" Activates: user-rules + abap-rules + performance/auditing

" Manual ABAP activation
" @abap-rules
" Force activates: user-rules + abap-rules
```

---

## 15. SAP RULE ACTIVATION LOGGING

```abap
" SAP Rule activation logging for debugging
CLASS zcl_sap_rule_logger DEFINITION.
  PUBLIC SECTION.
    CLASS-METHODS:
      log_active_sap_rules
        IMPORTING
          context TYPE ty_sap_context_detection,
      log_manual_sap_trigger
        IMPORTING
          trigger TYPE string
          activated_rules TYPE string_table.
ENDCLASS.

CLASS zcl_sap_rule_logger IMPLEMENTATION.
  METHOD log_active_sap_rules.
    " Log base rules
    WRITE: 'Base rules: abap-rules'.
    
    " Log SAP-specific rules
    IF context-abap = abap_true.
      WRITE: 'ABAP rules: abap-rules (dual activation)'.
    ENDIF.
    IF context-performance = abap_true.
      WRITE: 'Performance rules: sap-performance/auditing'.
    ENDIF.
  ENDMETHOD.
  
  METHOD log_manual_sap_trigger.
    LOOP AT activated_rules INTO DATA(rule).
      WRITE: rule.
    ENDLOOP.
  ENDMETHOD.
ENDCLASS.
```

---

> Actualiza este archivo conforme surjan nuevos patrones o restricciones corporativas ABAP.