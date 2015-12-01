
########################################################################################
#############               ���� pic_conversion ���ļ�                          ############## 
########################################################################################
LIST (APPEND pic_conversion_LIB_SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/convert.c
    )
    

 
########################################################################################
#############               ���� pic_conversion ��汾��                        ############## 
########################################################################################
set(pic_conversion_LIB_VERSION     "1.0.0")
set(pic_conversion_LIB_SOVERSION   "1")


   
########################################################################################
#############              ����ͷ�ļ�Ŀ¼                                 ############## 
########################################################################################
include_directories(  
    ${PROJECT_SOURCE_DIR}/includes  
    ${PROJECT_SOURCE_DIR}/Views
    ${PROJECT_SOURCE_DIR}/Views/PicConversion
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
IF (MODULE_pic_conversion)
    #���ɶ�̬��  ��̬���� STATIC  
    add_library (pic_conversionlib SHARED      ${pic_conversion_LIB_SRCS})  
    add_library (pic_conversions   STATIC      ${pic_conversion_LIB_SRCS})  
    
    # ���ð汾�ţ�SOVERSIONΪAPI�汾��
    set_target_properties(pic_conversionlib   PROPERTIES 
                                        VERSION     ${pic_conversion_LIB_VERSION} 
                                        SOVERSION   ${pic_conversion_LIB_SOVERSION} )
ELSE (MODULE_pic_conversion)
    MESSAGE(STATUS "Not Include pic_conversion module.")
ENDIF (MODULE_pic_conversion)



########################################################################################
#############                 ����Ŀ�������ļ�                          ############## 
########################################################################################
IF (TEST_MODULE_FLAG AND MODULE_pic_conversion)
    add_executable(TestPicConversion.elf    pic_conversionTest.c)
    add_dependencies(TestPicConversion.elf      loglib  viewslib pic_conversionlib )
    target_link_libraries(TestPicConversion.elf loglib  viewslib pic_conversionlib )

ELSE (TEST_MODULE_FLAG AND MODULE_pic_conversion)
    MESSAGE(STATUS "Not Include pic_conversion module.")
ENDIF (TEST_MODULE_FLAG AND MODULE_pic_conversion)



