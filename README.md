# 2_NeuralNetwork

->super(Net, self).__init__()을 쓰는 이유

만약, Net이 Module과 operation을 상속받고, 이 두개의 class는 A를 상속받을 때,
super(Net, self).__init__()을 쓰지 않으면, Module, Operation, A를 init할 수 없다.
Parent class를 init하지 않으면, 나중에 문제가 생길 수 있음.

self는 Net의 instance 객체이다.
요기서 self를 쓰는 이유는,
super(Net, self).__init__()을 부르면, super(Module, self).__init__(),super(Operation, self).__init__()이 호출된다.
이로인해, 이것은 A의 __inint__()을 두 번 부르게 되는데 이것은 문제를 야기한다.
그래서, (class_name, self)에서 class_name과 self가 같지 않으면, super(class_name, self).__init__()을 삭제한다.
즉, super(Module, self).__init__(),super(Operation, self).__init__()은 삭제되어 진다.

간단히 말하자면, super(Net, self).__init__()을 부르면, Net이 상속받은 모든 부모 클래스가 초기화되는 것이라고 기억하자.


->batch를 사용하는 이유

MNIST data 1,1,1,1,7,1 이 모두 1이라고 labeling되어 있다고 하자.

만약, batch=1 이라고 가정라면, 
5번째 데이터를 보고 학습하여 7을 1이라고 생각할 수 도 있다.

하지만 batch 사이즈를 지정하여 여러 개의 데이터를 함께 학습하다보면, 다섯 번째 데이터가 1이 아니라는 것을 알아낼 수 있다.
이러한 이유에서 우리는 batch size를 지정한다.

-> Interface

torch.randn(1,1,32,32)는 우리가 사용하기 쉽게 만들어진 interface이다. 
이 뒤의 구조는 1차원의 배열로 되어 있다.

우리는 forward()함수에서 view함수를 사용하여, 데이터를 일자로 쭉 펴주었는데, 
이것은 원래 데이터는 1차원이었지만, 이제 데이터를 1차원이라고 생각하라는 interface차원의 코드이다. ("우리는 이제 데이터를 1차원으로 쭉 펴서 사용할꺼야!")







