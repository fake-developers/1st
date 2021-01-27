# [GIT] Git 브랜치 전략 (GitHub flow, Git flow)

:writing_hand: *Assembled by JiYoung-Kwon (2021-01-25)* 



#### :pushpin: Git 브랜치를 효과적으로 나누고, 관리하기

* **대표적인 브랜칭(branching) 전략**
  * Git-flow
  * GitHub-flow

#### :pushpin: Git vs GitHub

* Git 
  * 분산 소스 버전 관리 시스템
  * 서버를 분산시켜 구축할 수 있게 하는 소프트웨어
  * 소스코드를 효율적으로 관리할 수 있게 해주는 형상 관리 도구
* GitHub
  * 깃(Git)을 사용하는 프로젝트를 지원하는 웹호스팅 서비스
  * Git을 업로드 할 수 있는 웹사이트
  * 개발자들의 버전 제어 및 공동 작업을 위한 플랫폼

***



## 1. Git-flow

* 가장 최초로 제안된, 가장 유명한 Git 워크플로우

* [Vincent Driessen이 말한 branching model](http://nvie.com/posts/a-successful-git-branching-model/)를 구현한 Git 확장 모듈 - [nvie/gitflw](https://github.com/nvie/gitflow)

* 브랜치 전략에 있어서 다른 워크플로우보다 엄격함

  -> 대규모의 프로젝트를 관리하는데 적합한 것으로 평가받고 있음

* 기본 브런치는 5가지로 구분

  * `feature > develop > release > hotfix > master` 
  * 항상 유지되는 메인 브랜치들(master, develop)
  * 일정 기간 동안만 유지되는 보조 브랜치들(feature, release, hotfix)
    * 머지된 `feature`, `release`, `hotfix` 브런치는 삭제
  * **master** : 제품으로 출시될 수 있는 브랜치
  * **develop** : 다음 출시 버전을 개발하는 브랜치
  * **feature** : 기능을 개발하는 브랜치
  * **release** : 이번 출시 버전을 준비하는 브랜치
  * **hotfix** : 출시 버전에서 발생한 버그를 수정하는 브랜치

<br/>

#### 1-1. Git-flow

<img src = https://lh5.googleusercontent.com/YBoig12xGUyZKF3j9lNrPT_vuDqLvh2Y4snSSBL0UuILhBxvfJjXZRkhUTjmEQIJ_31GkQnsb5fTI3nSwmL8zAi3ZrpPm_QARYF1Q9IyooXdXL8CWiDxIyCl32JWmwFBL5J0Igli width=50%>

1. master와 develop 브랜치가 존재 (develop 브랜치는 master에서부터 시작된 브랜치)
2. develop 브랜치에서는 상시로 버그를 수정한 커밋들이 추가됨
3. 새로운 기능 추가 작업이 있는 경우
   * develop 브랜치에서 feature 브랜치를 생성 (feature 브랜치는 언제나 develop 브랜치에서부터 시작)

4. 기능 추가 작업이 완료되었다면
   * feature 브랜치는 develop 브랜치로 merge됨

5. develop에 이번 버전에 포함되는 모든 기능이 merge 되었다면
   * QA를 하기 위해 develop 브랜치에서부터 release 브랜치를 생성

6. QA를 진행하면서 발생한 버그들은 release 브랜치에서 수정

7. QA를 무사히 통과했다면
   * release 브랜치를 master와 develop 브랜치로 merge

8. 마지막으로 출시된 master 브랜치에서 버전 태그를 추가



#### 1-2.  메인 브랜치 (Main branch)

* master 브랜치와 develop 브랜치를 병행으로 유지

<img src = https://lh4.googleusercontent.com/CZlG9QPr4RYMGAJ3z2ihWV6UuyJRqEmYSwm4Du3AeaFCc2-lrrEG-rWA6YkWKyFvAye_uKv0123vXLt4JY_dey_KkDk8VdPAHvDOgzLg2pwTE0k6li-dL_YUWpP-8Ck8Xrbx4ouS width = 60%>

* **master**
  * 배포 가능한 상태만을 관리하는 브랜치
* **develop**
  * 다음에 배포할 것을 **개발**하는 브랜치
  * develop 브랜치는 통합 브랜치의 역할을 하며, 평소에는 이 브랜치를 기반으로 개발을 진행

<br/>

#### 1-3. 보조 브랜치 (Supporting branch)

* **feature**

  <img src = https://lh6.googleusercontent.com/J9X6SYLWwSLiLb6JAd_HBMFeTXpzwIZIMUkqtJpXZzi5cg42gIHLx3F99X-wSVIoFEc0u7NCY08yl-xTFolFlwfR0ytJWxZntoZS3-5WWq_oAlIO_MfJWKQfQYur_8ed7D_vzPF3 width = 60%>

  > * 갈라져 나온 브랜치 :  develop
  > * 다시 merge할 브랜치 : develop
  > * 브랜치 이름 규칙 : master, develop, release-\*, hotfix-\*를 제외한 것
  * 기능을 개발하는 브랜치로, develop 브랜치로부터 분기
  * 기능을 다 완성할 때까지 유지하고, 다 완성되면 develop 브랜치로 merge

  <br/>

  :bulb: develop 브랜치, feature 브랜치

  * 기존에 잘 작동하는 개발 코드(develop 브랜치)와 새로 변경될 개발코드(feature 브랜치)를 분리하고 각각 보존하는 것
  * feature 브랜치는 Git-flow 전략에서 지칭하는 단위 개발 브랜치의 의미를 가짐

<br/>

* **release**

  <img src = https://lh5.googleusercontent.com/4mXmoEov9sqhCEo6vxFF8eOrvrc5hyo0SvW6YLgJMoauuejV0ketnm9yxjc1JyiUqjZnWwMCQr71JATvU1mAlxk3NPrQcglpWTpaIbIL1aiJbVXJ2e4DSocSo5eeG_I6zOQVfZ9A width = 60%>

  > * 갈라져 나온 브랜치 : develop
  > * 다시 merge할 브랜치 : develop, master
  > * 브랜치 이름 규칙 : release-*

  * develop 브랜치에 이번 버전에 포함되는 기능이 merge 되었다면 QA를 위해 develop 브랜치에서부터 release 브랜치를 생성
  * 배포를 위한 최종적인 버그 수정 등의 개발을 수행
  * 배포 가능한 상태가 되면  master 브랜치로 병합시키고, 출시된 master 브랜치에 버전 태그를 추가
  * release 브랜치에서 기능을 점검하며 발견한 버그 수정 사항은 develop 브랜치에도 적용해 주어야함! 그러므로 배포 완료 후 develop 브랜치에 대해서도 merge 작업을 수행

<br/>

* **hotfix**

  <img src =https://lh5.googleusercontent.com/_jcNDU-WEGylP-1Z5CFOIYBDjwOmaqUi6DslzKGZ39rts9IXEEBdyq7NvF1jrlXnLg2dn_mL-tnvINUrUFSx4UOlAkOov_EpwW6eF1zRHYEK8xRB__GyG5HrpEWWFjHNa23WhF8I width = 60%>

  > * 갈라져 나온 브랜치 : master
  > * 다시 merge할 브랜치 : develop, master
  > * 브랜치 이름 규칙 : hotfix-*

  * 배포한 버전에서 긴급하게 수정을 해야 할 필요가 있을 경우, master 브랜치에서 분기하는 브랜치
  * 버그를 잡는 사람이 일하는 동안에도 다른 사람들은 develop 브랜치에서 하던 일을 계속 할 수 있음
  * 이 때 만든 hotfix 브랜치에서의 변경 사항은 develop 브랜치에도 merge하여 문제가 되는 부분을 처리해 주어야 함

<br/>

#### 1-4. Git-flow의 장단점

##### **장점**

- 명령어가 명료하게 나와있다.
- 거의 모든 에디터들과 IDE들에 플러그인으로서 이미 존재하고 있다.

##### **단점**

- branch가 많아 뻗어나가는 구조가 복잡하여 관리 등에 어려움이 있다.
- 몇몇 branch는 쓰이지 않을 경우가 있다. 그리고 애매한 포지션의 branch가 존재한다.



## 2. GitHub-flow

![img](https://lh3.googleusercontent.com/h5H7FB2-aBPVThE4ZlZt919Fl9CstlD17NlJoODMKOlMEHmEV0encsCR2KmJ4yc6JwMsqoyv7u3jWVtW17Q3EqcHzPxUya85fRwRjgDlL2BapLtarQiu-SnjpUjyC2weng-PAXwx)

* Git-flow가 깃헙에서는 사용하기 복잡하다고 하여 나온 브랜칭 전략, Scott Chacon
* Git flow에 비해 흐름이 단순해짐에 따라 그 규칙도 단순해짐
* master branch에 대한 규칙만 정확하게 정립되어 있다면, 나머지 브랜치들에 대해서는 관여하지 않음
  * 즉, hotfix 브랜치나 feature 브랜치를 구분하지 않음
* pull request 기능을 사용하도록 권장함
* **자동화 개념이 들어가 있다**라는 큰 특징이 존재함
  * 만일 자동화가 적용되어 있지 않은 곳에서만 수동으로 진행하면 됨
* 수시로 배포가 일어나며, CI와 배포가 자동화되어 있는 프로젝트에 유용
  * CI : 개발자를 위한 자동화 프로세스인 지속적인 통합(Continuous Integration)을 의미

<br/>

#### 2-1. 특징

* release 브런치가 명확하지 않은 시스템에서 사용에 맞게 되어 있음

  * GitHub의 서비스 특성상 릴리즈라는 개념이 없는 서비스를 진행하고 있기 때문

  * 웹 서비스들이 릴리즈라는 개념이 없어지고 있으니 사용하기 편할 것
* hotfix와 가장 작은 기능을 구분하지 않음
  * 어차피 둘 다 개발자가 수정해야 되는 일중에 하나
  * 단지 우선순위가 어디가 높냐의 차이

<br/>

#### 2-2. 사용법

1. **master 브랜치는 어떤 때든 배포가 가능하다**

   * master 브랜치는 항상 최신 상태이며, stable한 상태로 product 에 배포되는 브랜치
   * 엄격한 규칙을 지정하여 사용
   * merge 전에 충분한 테스트를 거쳐야 함

   ![img](https://lh4.googleusercontent.com/vsBcwTwsJPJ-t9vnyCvs4lmrC_P0Qke7ZFjT10Mk7O_t12TL_HmpZba5jgy89Byc646rtiY-X7O9p19uuf9JKnEaSRWn8flR54gx5QILtJs12Di36AtXNX94e6jYyPHz7LGsY9sb)

2. **master에서 새로운 일을 시작하기 위해 브랜치를 만든다면 이름을 명확히 작성한다**

   * 브랜치는 항상 마스터 브랜치에서 만든다
   * Git-flow와 다르게 feature 브랜치나 develop 브랜치가 존재하지 않음
   * 새로운 기능을 추가하거나, 버그를 해결하기 위한 브랜치 이름은 자세하게 어떤 일을 하고 있는지에 대해서 작성해 주도록 한다
   * 커밋메세지를 명확하게 작성한다

   ![img](https://lh6.googleusercontent.com/gMQCUc-hAqLg5dDaZBtnrNgess1yecZYpBBTEvKt593QSgBn65sZsu6R02TJlQ2dLCvU5Mu8kWwsb-SuipcrNGlUrc4C8hDFVmCdqRnlH9HSrXkzFm5r8vxAo3fXRuAI8S0rj-DF)

3. **원격지 브랜치로 수시로 push 한다**

   * Git-flow와 상반되는 방식
   * 항상 원격지에 자신이 하고 있는 일들을 올려 다른 사람들도 확인할 수 있도록 해준다
   * 하드웨어에 문제가 발생해 작업하던 부분이 없어지더라도, 원격지에 있는 소스를 받아서 작업할 수 있도록 해준다

4. **피드백이나 도움이 필요할 때, merge 준비가 완료되었을 때에는 pull request를 생성한다**

   * pull request는 코드 리뷰를 도와주는 시스템
   * 자신의 코드를 공유하고 리뷰를 받는다
   * merge 준비가 완료되었다면 master 브랜치로 반영을 요구

   ![img](https://lh4.googleusercontent.com/-pI63MoIJs52pfVSy0XpfoVW1E7GX5nC6O6zuw84VJkDIHV_T9sj-RZ64OXB2zPKB-ENi8shIVHBM5JtNK8Jm2Mhz8uwcNznia5p1LTHJhTJg5aaVESezpMvBZUXoEIkD_-5xvqT)

5. **기능에 대한 리뷰와 논의가 끝난 후 master로 merge한다**

   * 곧장 product로 반영될 기능이므로, 이해관계가 연결된 사람들과 충분한 논의 이후 반영하도록 한다
   * CI도 통과해야 한다.

   ![img](https://lh3.googleusercontent.com/Ducuao3rKSP3QqqtUbpVE1Stnowm0pCAOdDOrAbvcDxpL03_YDAy0jL5-DDc67hmODgqTzjppiXnwUXsEXW-gSbLsuV5ZrPyen8unwDDnXs6591rLqsLjmGWa_v4hHv7turOaMGy)

6. **master로 merge되고 push 되었을 때는, 즉시 배포되어야 한다**

   * Github-flow 의 핵심
   * master로 merge가 일어나면 자동으로 배포가 되도록 설정해놓는다

   ![img](https://lh4.googleusercontent.com/-PWiMUHR0_sYymhKuYZQWBbhC7IrRDnlzjquGLR4i7XLT_8oYFrQe373kud7guoEh7lDtJBuYkxUV_V7sJA3hqsstHMq5Ndeio34wUsX_4E38jyO7UToJS67Gxk3tFCoEwdhM6Wf)

<br/>

#### 2-3. GitHub-flow의 장단점

##### **장점**

- branch 구성 전략이 단순하다.
- 처음 git을 접하는 사람에게 정말 좋은 시스템이 된다.
- Github 사이트에서 제공하는 기능을 모두 사용하여 작업을 진행한다.
- 코드 리뷰를 자연스럽게 사용할 수 있다.
- CI가 필수적이며, 배포는 자동으로 진행할 수 있다.
- Github가 작업을 할 때 이렇게 작업하고 있다.

##### **단점**

- CI와 배포 자동화가 되어있지 않은 시스템에서는 사람이 직접 관련된 업무를 진행해야 한다.
- 프로젝트 규모가 커짐에 따라 점점 관리에 어려움이 발생할 수 있다.

<br/>

## :page_with_curl: Reference

[Git 브랜칭 전략 : Git-flow와 Github-flow](https://hellowoori.tistory.com/56)

[우린 Git-flow를 사용하고 있어요](https://woowabros.github.io/experience/2017/10/30/baemin-mobile-git-branch-strategy.html)

[Git Flow와 GitHub Flow의 이해](https://codingtrainee.tistory.com/156)

[Git flow, GitHub flow, GitLab flow](https://ujuc.github.io/2015/12/16/git-flow-github-flow-gitlab-flow/)

[깃(Git)과 깃허브(GitHub) 궁금하시죠?](https://m.blog.naver.com/PostView.nhn?blogId=acornedu&logNo=221522579114&proxyReferer=https:%2F%2Fwww.google.com%2F)
