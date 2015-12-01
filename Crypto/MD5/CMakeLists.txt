########################################################################################
#############               ���� md5c ���ļ�                            ############## 
########################################################################################
LIST (APPEND md5c_LIB_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/md5c.c
    )
    
  
           
########################################################################################
#############               ���� md5 ��汾��                          ############## 
########################################################################################
set(md5_LIB_VERSION     "1.0.0")
set(md5_LIB_SOVERSION   "1")


  
########################################################################################
#############              ����ͷ�ļ�Ŀ¼                                 ############## 
########################################################################################
include_directories(  
    ${PROJECT_SOURCE_DIR}/includes
    ${PROJECT_SOURCE_DIR}/Crypto
    ${PROJECT_SOURCE_DIR}/Crypto/MD5
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
IF (MODULE_md5c)
    #���ɶ�̬��  ��̬���� STATIC  
    add_library (md5clib    SHARED          ${md5c_LIB_SRCS})  
    add_library (md5cs      STATIC          ${md5c_LIB_SRCS})  
    # ���ð汾�ţ�SOVERSIONΪAPI�汾��
    set_target_properties(md5clib   PROPERTIES 
                                    VERSION     ${md5_LIB_VERSION}
                                    SOVERSION   ${md5_LIB_SOVERSION} )
ELSE (MODULE_md5c)
    MESSAGE(STATUS "Not Include md5c module.")
ENDIF (MODULE_md5c)




########################################################################################
#############                 ����Ŀ�������ļ�                          ############## 
########################################################################################
IF (TEST_MODULE_FLAG AND MODULE_md5c)
    add_executable(TestMd5.elf  md5Test.c)
    add_dependencies(TestMd5.elf        md5clib  loglib)
    target_link_libraries(TestMd5.elf   md5clib loglib )

ELSE (TEST_MODULE_FLAG AND MODULE_md5c)
    MESSAGE(STATUS "Not Include md5c module.")
ENDIF (TEST_MODULE_FLAG AND MODULE_md5c)



