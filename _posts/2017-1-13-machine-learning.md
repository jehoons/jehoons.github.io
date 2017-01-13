### LSTM 네트워크의 이해
#### Recurrent Neural Networks
당신은 매 초마다 새로운 생각을 시작하는 것은 아니다. 이 글을 읽는 동안 당신은 이전 단어의 이해에 기반을 두어 단어들을 이해한다. 즉 당신은 모든 생각을 던져 버리고 새로운 생각을 시작하지 않는다는 것이다. 그러므로 당신의 생각은 지속성을 가지고 있다.

전통적 뉴럴네트워크는 이것을 할 수 없으며, 이는 주요한 결점인 것 처럼 보인다.

 
   For example, imagine you want to classify what kind of event is happening at every point in a movie. It’s unclear how a traditional neural network could use its reasoning about previous events in the film to inform later ones.

Recurrent neural networks address this issue. They are networks with loops in them, allowing information to persist.