# Item.1 생성자 대신 정적 팩터리 메서드를 고려하라

### 정적 팩토리 메서드(Static Factory Method)
- 객체의 생성을 담당하는 클래스 메서드
- 클래스 내에 선언되어 있는 메서드를 내부의 new를 이용해 객체를 생성해 반환
```
public static Boolean valueOf(boolean b) {
  return b ? Boolean.TRUE : Boolean.FALSE;
}
```
### 장점
1. 이름을 가질 수 있다.
2. 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다. (불변 클래스)
3. 반환 타입의 하위 타입 객체를 반환할 수 있는 능력
4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.
5. 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.

### 단점
1. 상속을 하려면 public이나 protected생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.
   - 상속보단 컴포지션(포함)을 사용하도록 유도하고 불변타입을 만들려면 제약을 지켜라라는 장점?
2. 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.

# Item.2 생성자에 매개변수가 많다면 빌더를 고려하라
매개변수가 많을때 사용
ex)
```
public class NutritionFacts {
  private final int servingSize;
  private final int servings;
  private final int calories;
  private final int fat;
  private final int sodium;
  private final int carbohydeate;

  public static class Builder {
    //필수 매개변수
    private final int servingSize;
    private final int servings;

    //선택 매개변수 - 기본값 초기화
    private int calories = 0;
    private int fat = 0;
    private int sodium = 0;
    private int carbohydrate = 0;

    public Builder(int servingSize, int servings){
      this.servingSize = servingSize;
      this.servings = servings;
    }

    pulbic Bulider calories(int val) {
      calories = val;
      return this;
    }

    
}
```
