Android Intent
============

1. Overview
------

 * Android Intent��Ŀ����Ϊ�˸��������ṩһ��ͨ��js������android�ֻ�������һ��intent�ķ�����
 * Web Intent��
     Web Intent��������android intent��һ�����ƣ���������Ŀ�Ļ�������web������web��ģ��android intent��
 * Android Intent��
     Android Intent��һ����android�ֻ�������intent�ķ�ʽ��
 * �����㶹�԰ٱ������ԣ���Ҫ�ۺ����ֵ��ص㣬ʵ��һ��ͨ��js�ķ�ʽ�����ֻ�������һ��intent��

2. Design
------


    interface AndroidIntent { 
        attribute DOMString action; 
        attribute DOMString type; 
        attribute DOMString data; 
        attribute DOMString category; 
        attribute DOMString component; 
        attribute DOMString extras; 
        attribute long flags;

        void startActivity();
    };

3. Implementation
--------

    var component = "com.wandoujia.phoenix2/com.wandoujia.phoenix2.ui.WelcomeActivity";
    var extras = [];
 
    var item = {};
    item.key = "phoenix.intent.extra.USER_AGENT";
    item.value = "wandoujia";
    extras.push(item);

    var i = new AndroidIntent("","","",
                             JSON.stringify(category),
                             component,
                             JSON.stringify(extras));
    // i.setFlags(0);

    i.startActivity();

4. ����ֵ
--------
 ���� startActivity() ����ֵ���£�
 <pre>
   "PERMISSION_DENY"  ��Ȩʹ�ø� intent
   "NOT_USB"          �� intent ��Ҫ usb ģʽ
   "NOT_CONNECTED"    ���ֻ�����
   "OK"               intent ���ͳɹ�
 </pre>

5. ���������ĺ�����android intent�ĺ���һ�£�
----
* action
 - ACTION_CALL
 - ACTION_EDIT
 - ACTION_MAIN
 - ACTION_SYNC
 - ACTION_BATTERY_LOW
 - ACTION_HEADSET_PLUG
 - ACTION_SCREEN_ON
 - ACTION_TIMEZONE_CHANGED

* type
 - ��ʽָ��Intent���������ͣ�MIME��
* data
 - ִ�ж���Ҫ����������
* category
 - ��ִ�ж����ĸ�����Ϣ����ʽΪjson

* Constant
 - CATEGORY_BROWSABLE
 - CATEGORY_GADGET
 - CATEGORY_HOME
 - CATEGORY_LAUNCHER
 - CATEGORY_PREFERENCE

 

* component
 - ָ��Intent�ĵ�Ŀ�������������
* extras
 - �������и�����Ϣ�ļ��ϣ���ʽΪjson

<pre>
 extra ���ݸ�ʽ�������£�
 {
   "key":"",
   "value":"",
   "type":""
 }

 ���� type ȡֵ���£�
 e    extra �е� value Ϊ string ����
 esn  extra �еĺ��� value ��ȡֵ
 ez   extra �е� value Ϊ bool ����
 ei   extra �е� value Ϊ int ����
 el   extra �е� value Ϊ long ����
 ef   extra �е� value Ϊ float ����
 eu   extra �е� value Ϊ uri ����
 ecn  extra �е� value Ϊ component name(ֻ�� usb ģʽ����ֵ��Ч)
 eia  extra �е� value Ϊ int array ����(�磺1, 2, 3)
 ela  extra �е� value Ϊ long array ����(�磺1, 2, 3)
 efa  extra �е� value Ϊ float array ����(�磺1.1, 2.1, 3)
 </pre>

* flags
 - ������������

 
6. Sample
------
* �ڵ�ͼ�ϲ�ѯ�ص�
<pre>
    var i = new AndroidIntent("android.intent.action.VIEW", // action
                         "", // type
                         "geo:0,0?q=shanghai", // data
                         "", // category
                         "", //component,
                         "");
    i.startActivity();
</pre>

* ������
<pre>
    var extras = [];
    var extra = {};
    extra.key = "sms_body";
    extra.value = "sms_body_test";
    extras.push(extra);

    var i = new AndroidIntent("android.intent.action.SENDTO", // action
                         "", // type
                         "sms:10086", // data
                         "", // category
                         "", //component,
                         JSON.stringify(extras));
    i.startActivity();
</pre>

* �������
<pre>
    var extras = [];
    var extra = {};
    
    // �����¼�������
    extra.key = "title";
    extra.value = "title_test";
    extras.push(extra);

    // �¼�������
    extra = {};
    extra.key = "description";
    extra.value = "description_test111";
    extras.push(extra);

    // �¼��Ŀ�ʼʱ��
    extra = {};
    extra.key = "beginTime";
    extra.value = "1351684995000";
    extra.type = "el";
    extras.push(extra);

    // �¼��Ľ���ʱ��
    extra = {};
    extra.key = "endTime";
    extra.value = "1351740880000";
    extra.type = "el";
    extras.push(extra);

    // ����Ƿ�Ϊ "ȫ��"
    extra = {};
    extra.key = "allDay";
    extra.value = "false";
    extra.type = "ez";
    extras.push(extra);

    // �¼��ĵص�
    extra = {};
    extra.key = "eventLocation";
    extra.value = "The gym";
    extras.push(extra);

    var i = new AndroidIntent("android.intent.action.EDIT",
                         "vnd.android.cursor.item/event",
                         "", // data
                         "", // category
                         "", //component,
                         JSON.stringify(extras));
    i.startActivity();
</pre>