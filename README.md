# fmti
File format identification

## ����
    make clean
    make
    �����ļ���
    fmti_test�����Գ���
    libfmti.so��
    ʹ�÷����� -L/usr/local/lib -lfmti
    
## API
    a) ��ʼ����FMTI_S *fmti_init();
    ���룺No
    ���أ�
        ʧ�� ---> NULL
        �ɹ� ---> ��NULL
    
    b) ����lib�⣺int fmti_load_lib(FMTI_S *p, char *path);
    ���룺
        p��FMTI_S�ṹ����
        path��signature·�����������ļ��л��ļ�
    ���أ�
        ʧ�� ---> ��0
        �ɹ� ---> 0
    
    c) ʶ���ļ���int fmti_file(FMTI_S *p, char *file_name, FMTI_MATCH_RESULT *match_res);
    ���룺
        p��FMTI_S�ṹ����
        file_name����Ҫʶ����ļ�·��
        match_res: ʶ����
    ���أ�
        ʶ������ļ�����ID
    
    d) �ͷ��ڴ棺void fmti_free(FMTI_S *p);

## ����signature
    ·����/etc/fmti/full
    ֧�����������չ
    fmti_load_lib(FMTI_S *p, char *path)
    �����������ļ��У�������ļ����µ�����sig�ļ�
    �����������ļ�����ֻ�������sig�ļ�
    
## ʶ�𷵻ر���
    fmti_fileֻ�����ļ����͵�id
    ������ø���ϸ����Ϣ��Ҫ����FMTI_MATCH_RESULT����
    
    a) PDFMT_S����ṹ��
    typedef struct
    {
        FMTI_LIB *lib;
        uint32_t lib_num;
    } FMTI_S;
    
    b) FMTI_MATCH_RESULT����ṹ��
    typedef struct
    {
        FMTI_LIB *match_lib;                     /* ƥ�䵽��signature��ΪNULL��signature��δ�鵽 */
        fmti_match_mode match_mode;              /* ���ʶ���ļ����� */
        uint32 id;                               /* �ļ�����id */
        uint32 priority;                         /* signature�����ȼ� */
        uchar ext[FMTI_FILE_EXT_SIZE + 1];      /* ���ļ�����չ�� */
        uint8 ext_match;                         /* ���ļ�����չ���Ƿ���signature�е���չ���Ƿ�ƥ�䣬1��ƥ�䣬0����ƥ�� */
    } FMTI_MATCH_RESULT;
    
    c) FMTI_LIB����ṹ��
    
    
## ����ʾ��
    FMTI_S *fmti;
    fmti = fmti_init();
    fmti_load_lib(fmti, "/etc/fmti/full");
    int filetype;
    filetype = fmti_file(fmti, "test.file");
    fmti_free(fmti);
