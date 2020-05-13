class ZCL_BAL_LOG definition
  public
  final
  create public .

public section.

  methods CONSTRUCTOR
    importing
      !OBJECT type BALOBJ_D
      !SUBOBJECT type BALSUBOBJ
      !EXTNUMBER type BALNREXT .
  methods ADD_MSG
    importing
      !MSGTY type SYMSGTY
      !MSGID type SYMSGID
      !MSGNO type SYMSGNO
      !MSGV1 type SYMSGV
      !MSGV2 type SYMSGV
      !MSGV3 type SYMSGV
      !MSGV4 type SYMSGV .
  methods SAVE .
protected section.
private section.

  data OBJECT type BALOBJ_D .
  data SUBOBJECT type BALSUBOBJ .
  data EXTNUMBER type BALNREXT .
ENDCLASS.



CLASS ZCL_BAL_LOG IMPLEMENTATION.


* <SIGNATURE>---------------------------------------------------------------------------------------+
* | Instance Public Method ZCL_BAL_LOG->ADD_MSG
* +-------------------------------------------------------------------------------------------------+
* | [--->] MSGTY                          TYPE        SYMSGTY
* | [--->] MSGID                          TYPE        SYMSGID
* | [--->] MSGNO                          TYPE        SYMSGNO
* | [--->] MSGV1                          TYPE        SYMSGV
* | [--->] MSGV2                          TYPE        SYMSGV
* | [--->] MSGV3                          TYPE        SYMSGV
* | [--->] MSGV4                          TYPE        SYMSGV
* +--------------------------------------------------------------------------------------</SIGNATURE>
  METHOD add_msg.
    DATA :
          ls_msg TYPE bal_s_msg.

    ls_msg-msgty = msgty .
    ls_msg-msgid = msgid .
    ls_msg-msgno = msgno .
    ls_msg-msgv1 = msgv1 .
    ls_msg-msgv2 = msgv2 .
    ls_msg-msgv3 = msgv3 .
    ls_msg-msgv4 = msgv4 .

    CALL FUNCTION 'BAL_LOG_MSG_ADD'
      EXPORTING
        i_s_msg          = ls_msg
      EXCEPTIONS
        log_not_found    = 1
        msg_inconsistent = 2
        log_is_full      = 3
        OTHERS           = 4.

  ENDMETHOD.


* <SIGNATURE>---------------------------------------------------------------------------------------+
* | Instance Public Method ZCL_BAL_LOG->CONSTRUCTOR
* +-------------------------------------------------------------------------------------------------+
* | [--->] OBJECT                         TYPE        BALOBJ_D
* | [--->] SUBOBJECT                      TYPE        BALSUBOBJ
* | [--->] EXTNUMBER                      TYPE        BALNREXT
* +--------------------------------------------------------------------------------------</SIGNATURE>
  METHOD constructor.
    DATA :
          ls_log TYPE bal_s_log.

    me->object = object.
    me->subobject = subobject.
    me->extnumber = extnumber.

    ls_log-object = object.
    ls_log-subobject = subobject.
    ls_log-extnumber = extnumber.

    CALL FUNCTION 'BAL_LOG_CREATE'
      EXPORTING
        i_s_log                 = ls_log
*    IMPORTING
*       e_log_handle            = l_log_handle
      EXCEPTIONS
        log_header_inconsistent = 1
        OTHERS                  = 2.

  ENDMETHOD.


* <SIGNATURE>---------------------------------------------------------------------------------------+
* | Instance Public Method ZCL_BAL_LOG->SAVE
* +-------------------------------------------------------------------------------------------------+
* +--------------------------------------------------------------------------------------</SIGNATURE>
  METHOD save.
    CALL FUNCTION 'BAL_DB_SAVE'
      EXPORTING
        i_save_all       = 'X'
      EXCEPTIONS
        log_not_found    = 1
        save_not_allowed = 2
        numbering_error  = 3
        OTHERS           = 4.
    IF sy-subrc <> 0.
      MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
      WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
    ENDIF.
  ENDMETHOD.
ENDCLASS.
