# ABAP RULES - EFFICIENCY FOCUSED

> Solo reglas ABAP que no domino automáticamente - corporate constraints y legacy compatibility.

---

## 🚨 **SAP CORPORATE CONSTRAINTS (I Don't Master)**

### **File System Restrictions**
- NO `.cursor/` folders allowed in SAP project directories
- NO carpetas ni subcarpetas
- NO archivos temporales fuera de /tmp
- Corporate restrictions on file system modifications

### **SSL/Proxy Requirements**
- SSL/Proxy requirements for external connections
- Corporate security policies compliance
- Legacy system compatibility requirements

### **Corporate Security Patterns**
```abap
" I don't know corporate authorization patterns automatically
IF NOT is_authorized( user ).
  MESSAGE e001(zmsg) WITH 'No authorization'.
  RETURN.
ENDIF.
```

---

## 🔄 **LEGACY SYSTEM COMPATIBILITY (I Don't Master)**

### **Legacy Compatibility**
- Mantener compatibilidad con versiones antiguas de SAP
- Usar solo funciones estándar

### **Migration Pattern**
```abap
" I don't know legacy migration patterns automatically
IF is_legacy_system( ).
  PERFORM legacy_process USING data.
ELSE.
  PERFORM modern_process USING data.
ENDIF.
```

---

## 🏗️ **RAP PATTERNS (I Don't Master)**

### **RAP (RESTful ABAP Programming)**
```abap
" I don't know RAP patterns automatically
CLASS zbp_my_rap_handler DEFINITION INHERITING FROM cl_abap_behavior_handler.
  PUBLIC SECTION.
    METHODS get_entity FOR READ BY KEY.
ENDCLASS.
```

---

## 🎯 **ABAP CONTEXT DETECTION (I Don't Master)**

### **ABAP Development Triggers**
```bash
# ABAP-specific triggers (manual activation)
@abap-development    # Activa todas las reglas ABAP
@rap-development     # Activa reglas específicas de RAP
@abap-corporate      # Activa reglas de restricciones corporativas
@abap-legacy         # Activa reglas de compatibilidad legacy
```

### **ABAP vs Web Development Context**
```typescript
// I don't know ABAP context detection automatically
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

## 🛡️ **SPECIAL CASES (I Don't Master)**

### **SAP CSV Format Standards**
- Headers on line 3 (SAP standard export format)
- Metadata in first 2 lines (system info, export timestamp)
- UTF-8 encoding with BOM for compatibility
- Corporate field naming conventions
- Mandatory audit fields (created_by, created_at, etc.)

### **Corporate Data Processing**
```abap
" I don't know corporate data processing patterns automatically
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

> Solo patrones ABAP específicos que no domino automáticamente.