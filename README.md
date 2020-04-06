# 기본 세팅

1.  reset.css ( styled-components의 경우 styled-reset )

    > 구글 검색해서 나오는 **reset.css**의 내용을 복사-붙여넣기 한 다음,
    >
    >     # styles.scss(css)
    >     @import "./reset.scss(css)";
    >
    > **styled**의 경우 createGlobalStyles 안에 styled-reset 패키지 설치 후
    >
    >        import reset from "styled-reset";
    >        export default createGlobalStyles`
    >           ${reset}
    >           ...
    >        `;
    >
    > 패키지를 설치할 여건이 안된다면, 아래와 같이라도 한다.
    >
    >     html, body {
    >        margin: 0;
    >        padding: 0;
    >     }

2.  box-sizing
    >     * {
    >        box-sizing: border-box;
    >     }
    >
    > > border, padding이 정해진 크기에서만 작동하게 만드는 설정

---

# 색상

1. #000 보다는 #333을 사용하자.

   > 완전 Black이 필요하다면 #000을 사용

2. #fff 보다는 다음과 같이 사용하자.

   - #f1f1f1
   - #f7f8f9

3. Main Color를 정하고, 거기에서 비슷한 색을 사용하자.

   > [여기](https://color.adobe.com/ko/create/color-wheel/)에서 **유사**, **단색**, **보색**, **혼합**, **음영** 등을 기준 색에 맞춰 확인할 수 있다.

4. gradient는 [여기](https://uigradients.com/#Firewatch)에서 색상을 가져와보자.

---

# 레이아웃

브라우저 크기에 비례하여 정확한 n등분 크기를 구현해야 하는 경우

두 가지 방법이 있다.

다음의 HTML 구조가 있다고 가정한다.

> ![carbon](https://user-images.githubusercontent.com/46839654/78560313-e7ce5f80-7850-11ea-87b7-335e692bc636.png)

1.  **flex**
    >     #app {
    >        display: flex;
    >     }
    >     .box {
    >        flex: 1;
    >     }
2.  **grid**
    >     #app {
    >        display: grid;
    >        grid-template-columns: repeat(3, 1fr);
    >     }

두 가지 방법 모두 결과는 동일하다.

> ![image](https://user-images.githubusercontent.com/46839654/78560724-793dd180-7851-11ea-80bd-4acc888e23b8.png)

만약 1번은 0.5, 2번은 1, 3번은 0.5로 설정해야 하는 경우

1.  **flex**

    >     #app {
    >        display: flex;
    >     }
    >     .box:first-child, .box:last-child {
    >        flex: 0.5;
    >     }
    >     .box:nth-child(2) {
    >        flex: 1;
    >     }

2.  **grid**
    >     #app {
    >        display: grid;
    >        grid-template-columns: 0.5fr 1fr 0.5fr;
    >     }

이 것 역시 두 가지 방법 모두 결과는 동일하다.

> ![image](https://user-images.githubusercontent.com/46839654/78561544-e140e780-7852-11ea-9f6f-0700f8ca1634.png)

1번 박스는 왼쪽 정렬, 2번 박스는 가운데 정렬, 3번 박스는 오른쪽 정렬을 하려면 다음과 같이 한다.

    #app {
        display: flex;
    }
    .box {
        display: flex;
    }
    .box:first-child {
        flex: 0.5;
    }
    .box:nth-child(2) {
        flex: 1;
        justify-content: center;
    }
    .box:last-child {
        flex: 0.5;
        justify-content: flex-end;
    }

> ![image](https://user-images.githubusercontent.com/46839654/78561892-6b894b80-7853-11ea-9da6-6d036479ff9f.png)

크로스 브라우징을 해야 한다면 grid 대신 flex로 사용하는 것이 정신건강에 좋다.
