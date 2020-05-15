- [기본 세팅](#%ea%b8%b0%eb%b3%b8-%ec%84%b8%ed%8c%85)
- [색상](#%ec%83%89%ec%83%81)
- [레이아웃](#%eb%a0%88%ec%9d%b4%ec%95%84%ec%9b%83)
  - [flex like grid](#flex-like-grid)
- [드롭다운 메뉴](#%eb%93%9c%eb%a1%ad%eb%8b%a4%ec%9a%b4-%eb%a9%94%eb%89%b4)
    - [HTML](#html)
    - [CSS](#css)
    - [HTML](#html-1)
    - [CSS](#css-1)
- [Skeleton UI](#skeleton-ui)
  - [단점](#%eb%8b%a8%ec%a0%90)
  - [설계](#%ec%84%a4%ea%b3%84)
  - [결론](#%ea%b2%b0%eb%a1%a0)
- [Autoresize Textarea](#autoresize-textarea)
  - [JSX](#jsx)
  - [CSS](#css-2)
  - [JS](#js)

---

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

---

# Skeleton UI

요즘 **skeleton**이 매우 핫합니다.

Loading Indicator를 보여주는 방법에는 여러가지가 있습니다.

그 중 대중적인 두 가지를 살펴 보겠습니다.

1. Loader
   > ![1](https://user-images.githubusercontent.com/46839654/80949627-4e827100-8e2f-11ea-909a-01ccbd352bad.gif)
2. Skeleton
   > ![2](https://user-images.githubusercontent.com/46839654/80949981-01eb6580-8e30-11ea-8139-f750455a2941.gif)

여러분은 두 가지 중에 어떤게 마음에 드시나요?

제가 속마음을 읽어보면 두 번째를 고르신 것 같습니다.

## 단점

이제 **Skeleton UI**를 설계하기 위해서는 조금 복잡해집니다.

**Loader**를 사용할 때에는 api로부터 받은 data가 존재하는지 확인하고 조건에 따라 내보내면 되었지만,

**Skeleton**을 사용할 경우에는 복합적으로 만들어야 합니다.

그러면 이제 만들어 보겠습니다.

## 설계

❗❗ **API에 대한 상세한 설명은 없음**

- Home Component

  >     const Home: React.FunctionComponent = () => {
  >       const { data } = useQuery<{ rooms: Array<_Query> }>(ROOMS);
  >       <Bottom>
  >         {!data ? (
  >         // * data가 존재하지 않으면 스켈레톤 보여줌
  >         <>
  >            {new Array(9).fill(1).map((_, index) => (
  >             <HomeSkeleton key={index} />
  >             ))}
  >         </>
  >         ) : null}
  >         {data?.rooms.map((item) => (
  >             // * data를 불러오면 mapping으로 뿌려줌
  >             <Card key={item.id}>
  >                 <CardLink to={`/room/${item.id}`}>
  >                     <div className="area-box">{item.area}</div>
  >                     <div className="info-box">
  >                         <span className="title">{item.title}</span>
  >                         {item.summary ? (
  >                         // * summary가 존재하면 보여주고 아니면 생략
  >                         <span className="summary">{item.summary}</span>
  >                         ) : null}
  >                         <span className="count">5명</span>
  >                     </div>
  >                 </CardLink>
  >             </Card>
  >         ))}
  >         </Bottom>
  >     }

- Skeleton (JSX)

  >     const HomeSkeleton: React.FunctionComponent = () => (
  >         <Card>
  >             <div className="area-box">
  >                 <div className="top skeleton"></div>
  >             </div>
  >             <div className="info-box">
  >                 <div className="info-1 skeleton"></div>
  >                 <div className="info-2 skeleton"></div>
  >                 <div className="info-3 skeleton"></div>
  >             </div>
  >         </Card>
  >     );

- Skeleton (SCSS)

  >     const Card = styled.div`
  >         display: flex;
  >         flex-direction: column;
  >
  >         & .skeleton {
  >             background-color: ${(props) => props.theme.bgColor.skeleton};
  >             border-radius: 5px;
  >         }
  >
  >         & .area-box {
  >             width: 100%;
  >             padding: 0 10px;
  >             & .top {
  >                 width: 100%;
  >                 height: 36px;
  >             }
  >         }
  >
  >         & .info-box {
  >             display: flex;
  >             flex-direction: column;
  >             padding: 10px;
  >
  >             & .info-1 {
  >                 width: 100%;
  >                 height: 16px;
  >                 margin-bottom: 10px;
  >             }
  >             & .info-2 {
  >                 width: 70%;
  >                 height: 14px;
  >                 margin-bottom: 10px;
  >             }
  >             & .info-3 {
  >                 width: 10%;
  >                 height: 14px;
  >             }
  >         }
  >     `;

## 결론

위와 같이 작업하면 다음과 같이 적용됩니다.

> ![2](https://user-images.githubusercontent.com/46839654/80949981-01eb6580-8e30-11ea-8139-f750455a2941.gif)

분명 **Loading Indicator**를 활용하는 것보다 매우 복잡합니다.

하지만 생각보다 괜찮은 효과를 줄 수 있습니다.

pure css로 만들기 힘드시면 **react-loading-skeleton**이라는 패키지가 있습니다.

직접 사용해보니 커스터마이징이 힘들어서 필자는 위와 같이 직접 만들어 사용합니다.

---

# Autoresize Textarea

![2](https://user-images.githubusercontent.com/46839654/82009665-e6435300-96aa-11ea-85d7-c6b60aeda199.gif)

textarea tag를 사용할 때 `react-autosize-textarea` 패키지를 사용하면 간편하게 만들 수 있긴 합니다만

직접 만들어 사용하는 것을 선호하므로 CSS + JS로 만들어 보겠습니다.

## JSX

    const Name: React.FunctionComponent = () => {
        const [description, setDescription] = useState<string>("");
        return (
            <Description>
                <span className="title">설명을 입력해주세요.</span>
                <textarea
                    id="description"
                    placeholder="내용 입력"
                    value={description}
                    onChange={textareaOnChange} >> value가 변경되어질 때마다 실행
                ></textarea>
            </Description>
        )
    }

## CSS

    const Description = styled.div`
        display: flex;
        flex-direction: column;
        align-items: center;

        & .title {
            font-size: 24px;
            margin-bottom: 15px;
        }
        & textarea {
            all: unset;
            width: 75%;
            height: 30px;
            line-height: 20px; ❗
            resize: none; ❗
            overflow: hidden; ❗
            border-bottom: 1px solid #bbb;
        }
    `;

## JS

❗❗ **Typescript로 작성되었습니다.**

✅ **Javascript로 개발하는 경우 `React.SynthicEvent~~`를 제거하고 `currentTarget --> target`으로 변경해야 합니다.**

    const textareaOnChange = (event: React.SyntheticEvent<HTMLTextAreaElement>) => {
        const { currentTarget } = event; ❗ event에서 target 추출
        setDescription(currentTarget.value); ❗ value 교체
        currentTarget.style.height = "1px";
        currentTarget.style.height = `${currentTarget.scrollHeight + 12}px`;
    };
