########################################################################################
#############               ���� md5lib ���ļ�                            ############## 
########################################################################################
LIST (APPEND md5lib_LIB_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/md5c.c
    )
    
  
           
########################################################################################
#############               ���� md5lib ��汾��                          ############## 
########################################################################################
set(md5lib_LIB_VERSION     "1.0.0")
set(md5lib_LIB_SOVERSION   "1")


  
########################################################################################
#############              ����ͷ�ļ�Ŀ¼                                 ############## 
########################################################################################
include_directories(  
    ${PROJECT_SOURCE_DIR}/includes
    ${PROJECT_SOURCE_DIR}/Crypto
    ${PROJECT_SOURCE_DIR}/Crypto/MD5lib
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
IF (MODULE_md5lib)
    #���ɶ�̬��  ��̬���� STATIC  
    add_library (md5liblib    SHARED          ${md5libc_LIB_SRCS})  
    add_library (md5libs      STATIC          ${md5libc_LIB_SRCS})  
    # ���ð汾�ţ�SOVERSIONΪAPI�汾��
    set_target_properties(md5liblib   PROPERTIES 
                                    VERSION     ${md5lib_LIB_VERSION}
                                    SOVERSION   ${md5lib_LIB_SOVERSION} )
ELSE (MODULE_md5lib)
    MESSAGE(STATUS "Not Include md5libc module.")
ENDIF (MODULE_md5lib)




########################################################################################
#############                 ����Ŀ�������ļ�                          ############## 
########################################################################################
IF (TEST_MODULE_FLAG AND MODULE_md5lib)
    add_executable(TestMd5lib.elf  md5libTest.c)
    add_dependencies(TestMd5lib.elf         md5liblib  loglib)
    target_link_libraries(TestMd5lib.elf   md5liblib loglib )

ELSE (TEST_MODULE_FLAG AND MODULE_md5lib)
    MESSAGE(STATUS "Not Include md5c module.")
ENDIF (TEST_MODULE_FLAG AND MODULE_md5lib)


