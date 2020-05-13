# abap_ballog

## Example

```
DATA :
      lo_bal_log          TYPE REF TO zcl_bal_log,
      
    CONSTANTS :
      lc_object       TYPE balobj_d  VALUE 'ILO15',
      lc_subobject    TYPE balsubobj VALUE 'VERIFICATION_RES_IN'
      lc_extnumber    TYPE balnrext VALUE 'XXXXX',.
      
    CREATE OBJECT lo_bal_log
      EXPORTING
        object    = lc_object
        subobject = lc_subobject
        extnumber = lc_extnumber.

     lo_bal_log->add_msg(
              EXPORTING
                msgty = sy-msgty        " Type de message
                msgid = sy-msgid        " Classe de messages
                msgno = sy-msgno        " Numéro du message
                msgv1 = sy-msgv1        " Variable de message
                msgv2 = sy-msgv2        " Variable de message
                msgv3 = sy-msgv3        " Variable de message
                msgv4 = sy-msgv4        " Variable de message
            ).

      lo_bal_log->save( ).
```
