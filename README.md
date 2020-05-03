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

## flex like grid

grid는 cross-browsing을 위해서라면 사용해선 안됩니다.

그렇지만 grid layout을 사용해야할 경우가 생기게 됩니다.

❗❗ grid처럼 완벽한 반응형 table을 만들 순 없습니다.

**HTML**

    <Bottom>
        <Card>
          <div className="area-box">A</div>
          <div className="info-box">content</div>
        </Card>
        <Card>
          <div className="area-box">B</div>
          <div className="info-box">content</div>
        </Card>
        <Card>
          <div className="area-box">C</div>
          <div className="info-box">content</div>
        </Card>
        <Card>
          <div className="area-box">D</div>
          <div className="info-box">content</div>
        </Card>
        <Card>
          <div className="area-box">E</div>
          <div className="info-box">content</div>
        </Card>
    </Bottom>

**SCSS**

    const Bottom = styled.div`
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    `;

    const Card = styled.div`
        display: flex;
        flex-direction: column;
        flex: 1 2 300px;
        border: 1px solid peru;
        margin: 10px;

    & .area-box {
        width: 100%;
        padding: 10px;
        background-color: skyblue;
    }
    `;

**Result**

> ![image](https://user-images.githubusercontent.com/46839654/80899061-5e725600-8d46-11ea-842b-89ab3038ec70.png)

이걸 grid로 바꾼다면 원하는 모양이 나옵니다.

    const Bottom = styled.div`
        display: grid;
        grid-template-columns: repeat(3, 1fr);
    `;

> ![image](https://user-images.githubusercontent.com/46839654/80899085-a85b3c00-8d46-11ea-8a8f-47a9d81c013b.png)

---

# 드롭다운 메뉴

profile_image를 클릭하거나 마우스를 갖다대면 메뉴가 나오게 만들어야하는 경우가 생긴다.

![optimize](https://user-images.githubusercontent.com/46839654/79357447-00d6bf00-7f7b-11ea-8caf-d33712ffffde.gif)

JS를 이용해서 만들 수도 있는데, pure css를 사용 해보겠다.

### HTML

    <body>
        <button>
            <img src="./sample.jpg" />
        </button>
        <div class="hover-box">
            Larry Jung
        </div>
    </body>

### CSS

    @keyframes anime {
        0% {
            opacity: 0;
            transform: translateY(-20px);
        }
        100% {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .hover-box {
        display: none;
        opacity: 0;
        width: 100px;
        height: 200px;
        background-color: #bbb;
        animation: anime 0.5s forwards;
    }

    button {
        all: unset;
        cursor: pointer;
    }

    img {
        width: 40px;
        height: 40px;
        border-radius: 50%;
    }

    button:focus + .hover-box { ❗ 클릭은 button:focus, hover는 button:hover ❗
        display: flex;
    }

주의할 점은 display: none >>> flex or block로 변경하게 되면

opacity나 transform 효과가 사라지기 때문에

effect를 줘야하는 element에 animation을 줘야한다.

✅ 기본값으로 `display: on, opacity: 0`인 경우에는 transition만 줘도 된다.

❗❗ **하지만** 이 상태로 끝나면 클릭 되었을 때, 보여진 item을 클릭할 수 없다.

이번에는 opacity가 증가하면서 내려오는 방식말고, 더 인터랙티브하게 바꿔보았다.

![ezgif com-optimize](https://user-images.githubusercontent.com/46839654/79847107-399eea00-83fa-11ea-8103-9bef14991805.gif)

### HTML

    <button>
      <img src="./sample.jpg" />
    </button>
    <div class="hover-box">
      Larry Jung
      <br />
      1
      <br />
      <button onclick="console.log('work')">click</button>
      <br />
      2
    </div>

### CSS

    @keyframes anime {
        0% {
            height: 0;
        }
        100% {
            height: 120px;
        }
    }

    .hover-box {
        display: none;
        flex-direction: column;
        width: 100px;
        height: 200px;
        background-color: #bbb;
        overflow: hidden;
        animation: anime 1s forwards;
    }

    button {
        all: unset;
        cursor: pointer;
    }

    img {
        width: 40px;
        height: 40px;
        border-radius: 50%;
    }

    button:hover + .hover-box,
    .hover-box:hover { // 👈 중요
        display: flex;
    }

드롭다운 메뉴가 드롭다운 박스에 마우스가 위치할 때에도 보여지게 해주면 된다.

React의 경우 상태 기반으로 드롭다운을 만드면 렌더링이 잦아진다.

이 과정을 CSS로 바꿔주면 코드가 짧아질 수 있다.
