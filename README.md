## �ٶ�ָ��ץȡ������ͼ��ʶ��õ�ָ��
### ��װ�Ŀ�ࣺܶ
>�ȸ�ͼ��ʶ��tesseract-ocr

>pip3 install pillow

>pip3 install pyocr

>selenium2.45

>Chrome47.0.2526.106 m or Firebox32.0.1

>chromedriver.exe

### ͼ��ʶ����֤����ο��ҵĲ��ͣ�
[pythonͼ��ʶ��--��֤��](http://www.cnblogs.com/TTyb/p/5996847.html)

### selenium�÷���ο��ҵĲ��ͣ�
[python֮selenium](http://www.cnblogs.com/TTyb/p/5842015.html)

### ����ٶ�ָ����Ҫ��½����½���˺�����д���ı�account���棺
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110153714827-1835068903.png)

### ���ܵ�½�������£�
```
# �������
def openbrowser():
    global browser

    # https://passport.baidu.com/v2/?login
    url = "https://passport.baidu.com/v2/?login&tpl=mn&u=http%3A%2F%2Fwww.baidu.com%2F"
    # �򿪹ȸ������
    # Firefox()
    # Chrome()
    browser = webdriver.Chrome()
    # ������ַ
    browser.get(url)
    # �������ʱ��
    # print("�ȴ�10��������...")
    # time.sleep(10)

    # �ҵ�id="TANGRAM__PSP_3__userName"�ĶԻ���
    # ��������
    browser.find_element_by_id("TANGRAM__PSP_3__userName").clear()
    browser.find_element_by_id("TANGRAM__PSP_3__password").clear()

    # �����˺�����
    # �����˺�����
    account = []
    try:
        fileaccount = open("../baidu/account.txt")
        accounts = fileaccount.readlines()
        for acc in accounts:
            account.append(acc.strip())
        fileaccount.close()
    except Exception as err:
        print(err)
        input("����ȷ��account.txt����д���˺�����")
        exit()
    browser.find_element_by_id("TANGRAM__PSP_3__userName").send_keys(account[0])
    browser.find_element_by_id("TANGRAM__PSP_3__password").send_keys(account[1])

    # �����½��½
    # id="TANGRAM__PSP_3__submit"
    browser.find_element_by_id("TANGRAM__PSP_3__submit").click()

    # �ȴ���½10��
    # print('�ȴ���½10��...')
    # time.sleep(10)
    print("�ȴ���ַ�������...")

    select = input("��۲��������վ�Ƿ��Ѿ���½(y/n)��")
    while 1:
        if select == "y" or select == "Y":
            print("��½�ɹ���")
            print("׼�����µĴ���...")
            # time.sleep(1)
            # browser.quit()
            break

        elif select == "n" or select == "N":
            selectno = input("�˺���������밴0����֤������밴1...")
            # �˺������������������
            if selectno == "0":

                # �ҵ�id="TANGRAM__PSP_3__userName"�ĶԻ���
                # ��������
                browser.find_element_by_id("TANGRAM__PSP_3__userName").clear()
                browser.find_element_by_id("TANGRAM__PSP_3__password").clear()

                # �����˺�����
                account = []
                try:
                    fileaccount = open("../baidu/account.txt")
                    accounts = fileaccount.readlines()
                    for acc in accounts:
                        account.append(acc.strip())
                    fileaccount.close()
                except Exception as err:
                    print(err)
                    input("����ȷ��account.txt����д���˺�����")
                    exit()

                browser.find_element_by_id("TANGRAM__PSP_3__userName").send_keys(account[0])
                browser.find_element_by_id("TANGRAM__PSP_3__password").send_keys(account[1])
                # �����½sign in
                # id="TANGRAM__PSP_3__submit"
                browser.find_element_by_id("TANGRAM__PSP_3__submit").click()

            elif selectno == "1":
                # ��֤���idΪid="ap_captcha_guess"�ĶԻ���
                input("�����������������֤�벢��½...")
                select = input("��۲��������վ�Ƿ��Ѿ���½(y/n)��")

        else:
            print("�����롰y�����ߡ�n����")
            select = input("��۲��������վ�Ƿ��Ѿ���½(y/n)��")
```

### ��½��ҳ�棺
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110154107624-1393804790.png)

### ��½������Ҫ���µĴ��ڣ�Ҳ���Ǵ򿪰ٶ�ָ���������л����ڣ���selenium�ã�
```
# �¿�һ�����ڣ�ͨ��ִ��js���¿�һ������
js = 'window.open("http://index.baidu.com");'
browser.execute_script(js)
# �´��ھ���л�������ٶ�ָ��
# ��õ�ǰ�����д��ڵľ��handles
# handlesΪһ������
handles = browser.window_handles
# print(handles)
# �л�����ǰ���´򿪵Ĵ���
browser.switch_to_window(handles[-1])
    
```

### �������򣬹�����������
```
# ��������
browser.find_element_by_id("schword").clear()
# д����Ҫ�����İٶ�ָ��
browser.find_element_by_id("schword").send_keys(keyword)
# �������
# <input type="submit" value="" id="searchWords" onclick="searchDemoWords()">
browser.find_element_by_id("searchWords").click()
time.sleep(2)
# ��󻯴���
browser.maximize_window()
# ��������
sel = int(input("��ѯ7���밴0��30���밴1��90���밴2�������밴3��"))
day = 0
if sel == 0:
    day = 7
elif sel == 1:
    day = 30
elif sel == 2:
    day = 90
elif sel == 3:
    day = 180
sel = '//a[@rel="' + str(day) + '"]'
browser.find_element_by_xpath(sel).click()
# ̫����
time.sleep(2)
```

### ����Ҳ�������
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110154603561-1092775179.png)

### �ҵ�ͼ�ο�
```
xoyelement = browser.find_elements_by_css_selector("#trend rect")[2]
```

### ͼ�ο���ǣ�
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110154817608-982142410.png)

### ���������Ĳ�ͬ����ƫ������
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110155142530-319352053.png)

### ѡȡ7����������۲죺
>��һ����ĺ�����Ϊ1031.66666

>�ڶ�����ĺ�����Ϊ1234
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110155720764-1186100464.png)

����7����������֮��Ĳ�Ϊ��202.33����������������

### ��selenium����ģ����껬��������
```
from selenium.webdriver.common.action_chains import ActionChains
ActionChains(browser).move_to_element_with_offset(xoyelement,x_0,y_0).perform()
```

### ����������ȷ���ĵ�ָ���������λ�ã�
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110155752202-120333333.png)

Ҳ���Ǿ��ε����Ͻǣ������ǲ������js��ʾ������ģ�����Ҫ��������+1��
```
x_0 = 1
y_0 = 0
```

### д������������ѭ�����ú������ۼӣ�
```
# ����ѡ�������ѭ��
for i in range(day):
    # �������
    if day == 7:
        x_0 = x_0 + 202.33
    elif day == 30:
        x_0 = x_0 + 41.68
    elif day == 90:
        x_0 = x_0 + 13.64
    elif day == 180:
        x_0 = x_0 + 6.78
```

### ������ʱ�ᵯ��������ַ�����ҵ������
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110160257592-723215476.png)

### selenium�Զ�ʶ��֮...��
```
# <div class="imgtxt" style="margin-left:-117px;"></div>
imgelement = browser.find_element_by_xpath('//div[@id="viewbox"]')
```

### ����ȷ�������Ĵ�Сλ�ã�
```
# �ҵ�ͼƬ����
locations = imgelement.location
print(locations)
# �ҵ�ͼƬ��С
sizes = imgelement.size
print(sizes)
# ����ָ����λ��
rangle = (int(locations['x']), int(locations['y']), int(locations['x'] + sizes['width']),
          int(locations['y'] + sizes['height']))
```

![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110160502389-924750650.png)

### �����˼·���ǣ�
>1. ��������Ļ��ͼ����

>2. �򿪽�ͼ������õ����������rangle���вü�

### �������ü���������������Ǹ��ڿ�����Ҫ��Ч���ǣ�
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110160724577-1831216031.jpg)

### ����Ҫ��rangle���м��㣬���������������������ʵĳ��ȣ�ֱ�ӱ�����д�ɣ�
```
# ����ָ����λ��
rangle = (int(locations['x'] + sizes['width']/3), int(locations['y'] + sizes['height']/2), int(locations['x'] + sizes['width']*2/3),
          int(locations['y'] + sizes['height']))
```

### ���д�����ղ�̫�ã�������Ҫ��keyword�ĳ��Ƚ����жϣ����ȹ����ᵼ�½�ͼ�������ƫ�������֪����ô�������ǲ�д���������ǿ���

### ��������������ǣ�
```
# <div class="imgtxt" style="margin-left:-117px;"></div>
imgelement = browser.find_element_by_xpath('//div[@id="viewbox"]')
# �ҵ�ͼƬ����
locations = imgelement.location
print(locations)
# �ҵ�ͼƬ��С
sizes = imgelement.size
print(sizes)
# ����ָ����λ��
rangle = (int(locations['x'] + sizes['width']/3), int(locations['y'] + sizes['height']/2), int(locations['x'] + sizes['width']*2/3),
          int(locations['y'] + sizes['height']))
# ��ȡ��ǰ�����
path = "../baidu/" + str(num)
browser.save_screenshot(str(path) + ".png")
# �򿪽�ͼ�и�
img = Image.open(str(path) + ".png")
jpg = img.crop(rangle)
jpg.save(str(path) + ".jpg")
```

### ���Ǻ��淢�ֲü���ͼƬ̫С��ʶ�𾫶�̫�ͣ�������Ҫ��ͼƬ��������
```
# ��ͼƬ�Ŵ�һ��
# ԭͼ��С73.29
jpgzoom = Image.open(str(path) + ".jpg")
(x, y) = jpgzoom.size
x_s = 146
y_s = 58
out = jpgzoom.resize((x_s, y_s), Image.ANTIALIAS)
out.save(path + 'zoom.jpg', 'png', quality=95)
```

ԭͼ��С�� **�Ҽ�->����->��ϸ��Ϣ** �鿴���ҵ��ǳ�73���أ���29����

### ������ͼ��ʶ��
```
# ͼ��ʶ��
index = []
image = Image.open(str(path) + "zoom.jpg")
code = pytesseract.image_to_string(image)
if code:
    index.append(code)
```

### ���Ч��ͼ��
![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110161512889-300916957.png)

![](http://images2015.cnblogs.com/blog/996148/201611/996148-20161110161525874-60911542.png)


## ��ϸ��˵��ۿ��ҵĲ��ͣ�
[TTyb](http://www.cnblogs.com/TTyb)