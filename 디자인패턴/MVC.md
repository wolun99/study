## MVC패턴

- Model,View,Controller로 이루어진 디자인 패턴입니다.
- 소프트웨어의 비지니스 로직과 화면을 구분하는데 중점을 두고 있습니다.
- 사용자가 Controller를 조작하면 model을 통해 데이터를 가져오고 그 데이터를 View를 통해 사용자에게 보여주는 과정을 가집니다.
- 대표적인 라이브러리는 React.js입니다.
- 장점 : 널리 사용하는만큼 단순합니다.
- 단점 : View와 Model 사이에 의존성이 높다.

### Model

- 애플리케이션이 포함해야 하는 데이터를 나타냄 즉, 데이터베이스, 상수, 변수 등을 뜻합니다.
- 상태가 변경되면 View에 알리며 가끔은 Controller에 알리기도 합니다.

### View

- 데이터를 보여주는 방식을 정합니다.
- Model이 가지고 있는 정보를 따로 저장하지 않아야 하며 단순히 화면에 표시가는 정보만 가지고 있어야 합니다.

### Controller

- 하나 이상의 모델과 하나 이상의 뷰를 잇는 다리 역할을 하며 메인 로직을 담당합니다.
- 변경을 감지하여 모델을 업데이트 할 필요없이 바로 처리할 수 있습니다.

### 동작방식

1. 사용자의 Action들은 Controller에 들어오게 됩니다.
2. Controller는 사용자의 Action를 확인하고, Model을 업데이트합니다.
3. Controller는 Model을 나타내줄 View를 선택합니다.
4. View는 Model을 이용하여 화면을 나타냅니다.

## MVP패턴

- MVC패턴에서 C에 해당하는 controller가 프레젠터(presenter)로 교체된 패턴입니다.
- 장점 : View와 Model사이에 의존성이 없습니다.
- 단점 : View와 Model사이에 의존성은 없어졌지만, View와 Presenter사이에 높은 의존성을 갖게 됬습니다.

### 프레젠터(presenter)

- View에서 요청한 정보를 Model을 가공해서 View에 전달해주는 부분

### 동작방식

1. 사용자의 Action들은 View를 통해 들어오게 됩니다.
2. View는 데이터를 Presenter에 요청합니다.
3. Presenter는 Model에게 데이터를 요청합니다.
4. Model은 Presenter에서 요청받은 데이터를 응답합니다.
5. Presenter는 View에게 데이터를 응답합니다.
6. View는 Presenter가 응답한 데이터를 이용하여 화면을 나타냅니다.

## MVVM패턴

- Model + View + View Model을 합친 용어로 다른 패턴들의 Model과 View의 의미가 같습니다.
- 대표적인 프레임워크는 Vue.js입니다.
- 장점 : View와 Model 사이에 의존성이 없습니다. 또한 View와 View Model 사이에 의존성을 없앴고, 각각 독립성을 가지고 있어 모듈화 하여 개발할 수 있습니다.
- 단점 : View Model 설계가 쉽지 않습니다.

### View Model

- View를 표현하기 위해 만든 View를 위한 Model

### 동작방식

1. 사용자의 Action들은 View를 통해 들어오게 됩니다.
2. View에 Action이 들어오면, Command 패턴으로 View Model에 Action을 전달합니다.
3. View Model은 Model에게 데이터를 요청합니다.
4. Model은 View Model에게 요청받은 데이터를 응답합니다.
5. View Model은 응답 받은 데이터를 가공하여 저장합니다.
6. View는 View Model과 Data Binding하여 화면을 나타냅니다.

### 특징

- Command패턴과 Data Binding 두가지 패턴을 사용했습니다.
  - Command : 여러가지 요소에 대한 처리를 하나의 액션으로 처리할 수 있게 하는 기법
  - Data Binding : 화면에 보이는 데이터와 웨 브라우저의 메모리 테이터를 일치시키는 기법, 뷰모델을 변경하면 뷰가 변경
- 두가지 패턴을 사용하여 View와 View Model 사이에 의존성을 없앴습니다.
