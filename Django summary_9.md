# 파이썬과 MariaDB 간 연동하기

> 1. 기본 설정
> 2. MariaDB와 연동하기



## 1. 기본 설정

```python
# config 폴더의 setting.py에서 경로 설정
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static')
]

UPLOAD_DIR = os.path.join(BASE_DIR,'static/img');
LOG_FILE = os.path.join(BASE_DIR,'log/mylog.log')
```

 * LOG_FILE에는 저장할 로그의 기본 이름과 위치를 지정한다.
   	* log 폴더는 프로젝트에서 위치한다.
   	* log 폴더에 mylog.log 파일을 만든다.
 * 만약 settings.py가 위치한 디렉토리를 기준으로 로그를 저장하려면 다음과 같이 코드를 입력한다.

```python
import os
LOG_FILE = os.path.join(os.path.dirname(__file__), '../log', 'myLog.log')
```



	* 원하는 위치를 지정하려면 아래와 같이 코드를 입력한다.

```python
# logging
LOGGING = {
    'version': 1,
    # 기존의 로깅 설정을 비활성화 할 것인가?
    'disable_existing_loggers': False,

    # 포맷터
    # 로그 레코드는 최종적으로 텍스트로 표현됨
    # 이 텍스트의 포맷 형식 정의
    # 여러 포맷 정의 가능
    'formatters': {
        'format1': {
            'format': '[%(asctime)s] %(levelname)s [%(name)s:%(lineno)s] %(message)s',
            'datefmt': '%d/%b/%Y %H:%M:%S'
        },
        'format2': {
            'format': '%(levelname)s %(message)s'
        },

    },

    # 핸들러
    # 로그 레코드로 무슨 작업을 할 것인지 정의
    # 여러 핸들러 정의 가능
    'handlers': {
        # 로그 파일을 만들어 텍스트로 로그레코드 저장
        'file': {
            'level': 'DEBUG',
            'class': 'logging.FileHandler',
            'filename': LOG_FILE,
            'formatter': 'format1',
        },
        # 콘솔(터미널)에 출력
        'console': {
            'level': 'DEBUG',
            'class': 'logging.StreamHandler',
            'formatter': 'format2',
        }
    },

    # 로거
    # 로그 레코드 저장소
    # 로거를 이름별로 정의
    'loggers': {
        'users': {
            'handlers': ['file'],
            'level': 'DEBUG',
        },
        'items': {
            'handlers': ['console'],
            'level': 'DEBUG',
        }
    },

}
```



## 2. MariaDB와 연동하기

> 1.  클래스 및 SQLite문 정의
> 2.  CRUD 함수 정의
> 3. views 파일에서 함수 정의



### 1) 클래스 및 SQLite문 정의

```python
import MySQLdb

# 동적 로딩을 통한 설정
config = {
    'database': 'shop',
    'user': 'root',
    'password': '111111',
    'host':'127.0.0.1',
    'port': 3306,
    'charset':'utf8',
    'use_unicode':True
}

class Db:
    def getConnection(self):
        conn = MySQLdb.connect(**config);
        return conn;

    def close(self, conn, cursor):
        if cursor != None:
            cursor.close();
        if conn != None:
            cursor.close();
```

 * 동적 로딩을 통한 설정은 자원 파일의 경로를 동적으로 등록하여 사용하는 방법이다.
   	* 파이썬 자원 파일을 프로젝트와 분리할 수 있는 장점을 나타낸다.
* 프로젝트 폴더에서 따로 폴더를 지정한 후에 자료를 저장할 데이터베이스, 클래스, SQLite문에 대한 파이썬 파일을 저장한다.



```python
class Sql:
    userlist = "SELECT * FROM usertb";
    userlistone = "SELECT * FROM usertb WHERE id= '%s' ";
    userinsert = "INSERT INTO usertb VALUES ('%s','%s','%s')";
------------------------------------------------------------------------------
class User:
    def __init__(self, id, pwd, name):
        self.id = id;
        self.pwd = pwd;
        self.name = name;
    def __str__(self):
        return self.id+' '+self.pwd+' '+self.name+' ';

class Item:
    def __init__(self, id, name, price, regdate, imgname):
        self.id = id;
        self.name = name;
        self.price = price;
        self.regdate = regdate;
        self.imgname = imgname;

    def __str__(self):
        return str(self.id) + ' ' + self.name + ' ' \
               + str(self.price) + ' '+ str(self.regdate) + ' '+self.imgname;
```



### 2) CRUD 함수 정의

```python
from frame.db import Db
from frame.sql import Sql
from frame.value import User


from frame.db import Db
from frame.sql import Sql
from frame.value import User


class UserDb(Db):

    def insert(self, id,pwd, name):
        try:
            conn = super().getConnection();
            cursor = conn.cursor();
            cursor.execute(Sql.userinsert % (id,pwd,name));
            conn.commit();
        except:
            conn.rollback();
            raise Exception;
        finally:
            super().close(conn, cursor);

    def update(self, id,pwd, name):
        try:
            conn = super().getConnection();
            cursor = conn.cursor();
            cursor.execute(Sql.userupdate % (pwd,name,id));
            conn.commit();
        except:
            conn.rollback();
            raise Exception;
        finally:
            super().close(conn, cursor);

    def delete(self, id):
        try:
            conn = super().getConnection();
            cursor = conn.cursor();
            cursor.execute(Sql.userdelete % (id));
            conn.commit();
        except:
            conn.rollback();
            raise Exception;
        finally:
            super().close(conn, cursor);

    def selectone(self,id):
        conn = super().getConnection();
        cursor = conn.cursor();
        cursor.execute(Sql.userlistone % id );
        u = cursor.fetchone();
        user = User(u[0],u[1],u[2]);
        super().close(conn, cursor);
        return user;

    def select(self):
        conn = super().getConnection();
        cursor = conn.cursor();
        cursor.execute(Sql.userlist);
        result = cursor.fetchall();
        all = [];
        for u in result:
            user = User(u[0],u[1],u[2]);
            all.append(user);
        super().close(conn,cursor);
        return all;

# userlist Test Function ................
def userlist_test():
    users = UserDb().select();
    for u in users:
        print(u);

def userlistone_test():
    users = UserDb().selectone('id01');
    print(users);
def userinsert_test():
    UserDb().insert('id04','pwd04','jeams');

if __name__ == '__main__':
    userinsert_test();
```

* 'if __name__ == '__main__''은 장고에서 클래스에서 정의한 함수를 시험할 때 시작 지점을 지정한다.
* CRUD 함수를 정의할 때 반드시 위와 같은 시험을 통해 정상적으로 작동하는 여부를 확인해야 한다.



```python
# views.py에서 html에서 사용할 함수를 정의

import logging
import os

from django.http import HttpResponseRedirect
from django.shortcuts import render, redirect

# Create your views here.
from django.utils.http import urlencode

from config.settings import BASE_DIR, UPLOAD_DIR
from frame import itemdb
from frame.error import ErrorCode
from frame.itemdb import ItemDb
from frame.userdb import UserDb
logger = logging.getLogger('users');

def userlist(request):
    #logger.debug('GET access User List....')
    rsuserlist = UserDb().select();
    context = {
        'section':'shop2/userlist.html',
        'rsusers':rsuserlist
    };
    return render(request, 'shop2/shop2.html',context)
def userdetail(request):
    id  = request.GET['id'];
    #logger.debug('user id:'+id)
    rsuser = UserDb().selectone(id);
    context = {
        'section': 'shop2/userdetail.html',
        'rsuser': rsuser
    };
    return render(request, 'shop2/shop2.html',context)

def useradd(request):
    context = {
        'section': 'shop2/useradd.html'
    };
    return render(request, 'shop2/shop2.html',context)

def userupdate(request):
    id = request.GET['id'];
    user = UserDb().selectone(id);
    context = {
        'section': 'shop2/userupdate.html',
        'uuser':user,
    };
    return render(request, 'shop2/shop2.html',context)

def userdelete(request):
    id = request.GET['id'];

    try:
        UserDb().delete(id);
    except:
        context = {
            'section': 'shop2/error.html',
            'error': ErrorCode.e0002
        };
        return render(request,'shop2/shop2.html',context);
    return redirect('userlist');

def userupdateimpl(request):
    id = request.POST['id'];
    pwd = request.POST['pwd'];
    name = request.POST['name'];
    try:
        UserDb().update(id,pwd,name);
    except:
        context = {
            'section': 'shop2/error.html',
            'error': ErrorCode.e0001
        };
        return render(request,'shop2/shop2.html',context);
    qstr = urlencode({'id': id})
    return HttpResponseRedirect('%s?%s' % ('userdetail', qstr))

def useraddimpl(request):
    id = request.POST['id'];
    pwd = request.POST['pwd'];
    name = request.POST['name'];
    try:
        UserDb().insert(id,pwd,name);
    except:
        context = {
            'section': 'shop2/error.html',
            'error': ErrorCode.e0001
        };
        return render(request,'shop2/shop2.html',context);
    return redirect('userlist');

class ItemView:
    def itemaddimpl(request):
        name = request.POST['name'];
        price = request.POST['price'];
        imgname = '';
        if 'img' in request.FILES:
            img = request.FILES['img']
            imgname = img._name

            fp = open('%s/%s' % (UPLOAD_DIR, imgname), 'wb')
            for chunk in img.chunks():
                fp.write(chunk);
                fp.close();

        ItemDb().insert(name,int(price),imgname);
        return redirect('itemlist');


    def itemlist(request):
        items = ItemDb().select();
        context = {
            'section': 'shop2/itemlist.html',
            'itemlist':items,
        };
        return render(request, 'shop2/shop2.html',context)
    def itemadd(request):
        context = {
            'section': 'shop2/itemadd.html'
        };
        return render(request, 'shop2/shop2.html',context)

    def itemdetail(request):
        id = request.GET['id'];
        item = ItemDb().selectone(int(id));
        context = {
            'section': 'shop2/itemdetail.html',
            'item':item,
        };
        return render(request, 'shop2/shop2.html', context)

    def itemupdate(request):
        id = request.GET['id'];
        item = ItemDb().selectone(int(id));
        context = {
            'section': 'shop2/itemupdate.html',
            'item':item,
        };
        return render(request, 'shop2/shop2.html', context)

    def itemupdateimpl(request):
        id = request.POST['id'];
        name = request.POST['name'];
        price = request.POST['price'];
        img = request.POST['img'];

        imgname = '';
        if 'newimg' in request.FILES:
            newimg = request.FILES['newimg']
            imgname = newimg._name

            fp = open('%s/%s' % (UPLOAD_DIR, imgname), 'wb')
            for chunk in newimg.chunks():
                fp.write(chunk);
                fp.close();
        else:
            imgname = img;

        ItemDb().update(int(id),name,int(price),imgname);
        qstr = urlencode({'id': id})
        return HttpResponseRedirect('%s?%s' % ('itemdetail', qstr))

class MainView:
    def login(request):
        context = {
            'section': 'shop2/login.html'
        };
        return render(request, 'shop2/shop2.html', context)

    def logout(request):
        if request.session['suser'] != None:
            del request.session['suser'];
        return render(request, 'shop2/shop2.html')

    def loginimpl(request):
        id = request.POST['id'];
        pwd = request.POST['pwd'];
        try:
            user = UserDb().selectone(id);
            if pwd == user.pwd:
                request.session['suser'] = id;
                context = {
                    'section': 'shop2/loginok.html',
                    'loginuser': user
                };
            else:
                raise Exception;
        except:
            context = {
                'section': 'shop2/error.html',
                'error': ErrorCode.e0003
            };
        return render(request, 'shop2/shop2.html', context);
```

 * pip install mysqlclient : python과 MySQL을 연결하는 라이브러리이다. 즉, 파이썬에서 MySQL 서버와 통신을 할 수 있게 하는 데이터베이스 커넥터( Databaser Connector)이다. 따라서 장고가 클라이언트 역할을 한다.
   	* C로 구현되어 있으며 똑같은 기능을 하는 pymysql에 비해 속도가 더 빠르다.
	* render는 새로운 화면을 출력하는 기능을, redirect는 인수로 받은 명령어를 다시 호출하는 기능을 한다.

