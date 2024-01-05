### AWS 인스턴스 성능테스트 (micro, nano, small, medium 순)
* 성능 테스트 크롤링 코드
```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    import requests
    from bs4 import BeautifulSoup

    # 여러 웹사이트의 URL 리스트
    urls = ['https://github.com/yeahh315',
            'https://github.com/Chaeniiiii',
            'https://github.com/Johyerin',
            'https://github.com/Woo-Shinyoung',
            'https://github.com/dbqudals',
            'https://github.com/kihyun1221',
            'https://github.com/seungtoctoc'
             ]
    
    result = ""

    for url in urls:
        # 각 웹사이트의 내용을 가져오기
        response = requests.get(url)

        # 가져온 내용을 BeautifulSoup을 사용하여 파싱
        soup = BeautifulSoup(response.text, 'html.parser')

        # <article> 태그 찾기
        article_tag = soup.find('article')
        name = soup.find('div', class_="vcard-names-container float-left js-profile-editable-names col-12 py-3 js-sticky js-user-profile-sticky-fields")
        
        result += url + "<br>"

        if name.text:
            result += name.text + "<br>"
        
        if article_tag:
            result += article_tag.text
        result += "<br>--------------------------------------------------<br><br>"

    if result:
        return result
    
    return ''



if __name__ == '__main__':
    app.run(host='0.0.0.0')

```
<br>

* Tg4 인스턴스 <br><br>
이러한 인스턴스는 기본 수준의 CPU 성능 외에 버스트 기능이 있어 워크로드에 필요한 만큼 성능을 높일 수 있습니다. 무제한 인스턴스는 필요할 때마다 원하는 기간 동안 높은 CPU 성능을 유지할 수 있습니다. 자세한 내용은 성능 순간 확장 가능 인스턴스 섹션을 참조하세요. 이러한 인스턴스는 다음의 경우에 적합합니다.<br><br>

    웹 사이트 및 웹 애플리케이션: <br>
    코드 리포지토리 <br>
    개발, 빌드, 테스트 및 스테이징 환경<br>
    마이크로서비스 <br><br>
    

* 인스턴스 별 성능 결과 <br><br>
<img width="444" alt="스크린샷 2024-01-04 오후 4 43 00" src="https://github.com/godltjsdud/godltjsdud/assets/71091090/a608481d-b5b9-45b2-be9c-61ce13ebd703"><br>
<img width="442" alt="스크린샷 2024-01-04 오후 4 35 46" src="https://github.com/godltjsdud/godltjsdud/assets/71091090/0875c67a-95e9-406a-99f3-ee7447939c8c"><br>
<img width="448" alt="스크린샷 2024-01-04 오후 4 29 42" src="https://github.com/godltjsdud/godltjsdud/assets/71091090/622e8732-2791-4a40-81ee-ba37289ec929"><br>
<img width="441" alt="스크린샷 2024-01-04 오후 4 51 42" src="https://github.com/godltjsdud/godltjsdud/assets/71091090/3a43c96a-01a1-4688-a4f9-13f45a2422b6"><br>
```
  t4g.micro : 5789ms 
  t4g.nano : 5989ms 
  t4g.small : 5810ms 
  t4g.medium :  6149ms

  micro < small < nano < medium
```
<br>

* 하드웨어 사양<br>
    | 인스턴스 유형 | 기본 vCPU | 메모리(GIB) |
    | ------- | ------- | ------- |
    | t4g.nano | 2 | 0.50 |
    | t4g.micro | 2 | 1.00 |
    | t4g.small | 2 | 2.00 |
    | t4g.medium | 2 | 4.00 |
