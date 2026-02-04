# Riverpod
Flutter에서 기존 Provider패키지의 한계를 극복하기 위해 설계된 상태 관리 라이브러리

## Riverpod의 장점
1. 컴파일 타임 안전성
- 앱을 실행하기 전 에러를 미리 알려줌
2. 의존성 주입의 편리성
- 위치 상관 없이 자유롭게 데이터를 사용함
3. 테스트 용이성
- MockData를 송출하기 쉽다


## Riverpod의 단점
1. 높은 초기 진입 장벽
- 필요한 도구가 많아 처음에 복잡함
2. 많은 코드량
- 아주 간단한 상태 하나를 만드는데도 작성해야할 기본 코드가 많음

### 사용 예시
```dart
import 'package:flutter/material.dart';
import 'package:flutter_riverpod/flutter_riverpod.dart';

// 1. 전역적으로 Provider 선언 (Scope에 구애받지 않음)
final counterProvider = StateProvider<int>((ref) => 0);

// 2. ConsumerWidget을 통해 상태 구독
class CounterPage extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // 3. ref.watch를 사용하여 상태값 감지 (값이 변하면 리빌드)
    final count = ref.watch(counterProvider);

    return Scaffold(
      body: Center(child: Text('$count')),
      floatingActionButton: FloatingActionButton(
        // 4. ref.read를 사용하여 상태값 변경 (이벤트 핸들러 내에서는 read 권장)
        onPressed: () => ref.read(counterProvider.notifier).state++,
        child: Icon(Icons.add),
      ),
    );
  }
}
```


**제미나이로 만든 쉬운 설명**
![alt text](riverpod.png)   
