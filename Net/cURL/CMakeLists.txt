########################################################################################
#############              ���� cURL ���ļ�                               ############## 
########################################################################################
LIST (APPEND cURL_LIB_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/cURL.c  
    )

    

########################################################################################
#############               ���� cURL ��汾��                          ############## 
########################################################################################
set(cURL_LIB_VERSION     "1.0.0")
set(cURL_LIB_SOVERSION   "1")

    
    
########################################################################################
#############              ����ͷ�ļ�Ŀ¼                                 ############## 
########################################################################################
include_directories(  
    ${PROJECT_SOURCE_DIR}/includes  
    ${PROJECT_SOURCE_DIR}/Network
    ${PROJECT_SOURCE_DIR}/Network/cURL
)  



########################################################################################
#############               ���� ���ӿ��ļ�Ŀ¼                           ############## 
########################################################################################
link_directories(  
    /usr/local/lib   
    )  


    
########################################################################################
#############           ����Ŀ����ļ� �� �����汾��                      ############## 
########################################################################################
IF (MODULE_cURL)

    #���ɶ�̬��  ��̬���� STATIC  
    add_library (cURLlib SHARED      ${cURL_LIB_SRCS})  
    add_library (cURLs STATIC        ${cURL_LIB_SRCS})  
    
    # ���ð汾�ţ�SOVERSIONΪAPI�汾��
    set_target_properties(cURLlib   PROPERTIES 
                                    VERSION     ${cURL_LIB_VERSION} 
                                    SOVERSION   ${cURL_LIB_SOVERSION} )
ELSE (MODULE_cURL)
    MESSAGE(STATUS "Not Include cURL module.")
ENDIF (MODULE_cURL)





########################################################################################
#############                 ����Ŀ�������ļ�                          ############## 
########################################################################################
IF (TEST_MODULE_FLAG AND MODULE_cURL)
    add_executable(TestcURL.elf    cURLTest.c)
    add_dependencies(TestcURL.elf          cURLlib loglib )
    target_link_libraries(TestcURL.elf     cURLlib loglib )

ELSE (TEST_MODULE_FLAG AND MODULE_cURL)
    MESSAGE(STATUS "Not Include cURL module.")
ENDIF (TEST_MODULE_FLAG AND MODULE_cURL)


