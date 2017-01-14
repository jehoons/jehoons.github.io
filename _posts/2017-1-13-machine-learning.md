---
title: 'LSTM 네트워크의 이해'
date: '2017-1-4 10:00'
layout: post
published: true
---
이 문서의 원문은 [여기](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)에서 확인할 수 있습니다. 좋은 내용이기 때문에 꼼꼼히 읽어보고 싶어서 번역합니다.

## LSTM 네트워크의 이해
### Recurrent Neural Networks
당신은 매 초마다 새로운 생각을 시작하는 것은 아닙니다. 이 글을 읽는 동안 당신은 이전 단어의 이해에 기반을 두어 단어들을 이해합니다. 즉 당신은 모든 생각을 던져 버리고 언제나 새로운 생각을 시작하지는 않습니다. 그로 인해 당신의 생각은 지속성을 가질 수 있게 됩니다.

전통적 신경망은 이러한 일을 할 수 없으며 큰 결점인 것 처럼 보입니다. 예를 들자면, 영화를 관람할 때 매 시간마다 어떤 종류의 이벤트가 발생하는지 분류하려고 한다고 상상해 봅시다. 전통적인 뉴럴네트워크를 이용하면 영화의 이전 사건에 대한 추론을 사용하여 어떻게 나중에 알려줄 (분류할 수) 수 있을지 확실하지 않습니다.

재귀신경망은 바로 이런 문제를 잘 처리할 수 있습니다. 재귀신경망들이 내부에 가지고 있는 피드백들때문에 정보가 지속적으로 처리되도록 할 수 있습니다.

<div style="text-align:center" markdown="1">
![](https://www.dropbox.com/s/3cxzh6z34utx9qw/RNN-rolled.png?dl=1){:height="200px" .center-image}

**그림.** 루프를 가지고 있는 재귀신경망
</div>

위 다이어그램에서, 신경망 묶음 $$A$$는 입력 $$X_t$$를 받아들이고 $$h_t$$를 출력으로 내보냅니다. 여기서 루프는 정보가 네트워크의 하나의 단계로부터 네트워크의 다음으로 통과하도록 허용합니다.

이러한 루프들은 재귀신경망을 다소 신비하게 보이도록 합니다. 반면, 조금 더 생각해보면, 보통의 뉴럴네트워크와 완전히 다르지는 않다는 것을 알게 됩니다. 재귀신경망은 동일한 네트워크의 여러 복사본으로 생각할 수 있으며 각각은 후임자 네트워크에게 메시지를 전달합니다. 루프를 풀면 어떻게 될지 한번 생각해 봅시다:

<div style="text-align:center" markdown="1">
![](https://www.dropbox.com/s/9n9r2ro3s5itb7c/RNN-unrolled.png?dl=1){:height="200px" .center-image}

**그림.** 루프를 푼 재귀신경망
</div>

이러한 재귀신경망의 체인같은 성질은 재귀신경망이 시퀀스와 리스트 데이터에 밀접하게 관련되어 있다는 것을 의미합니다. 즉, 시퀀스와 리스트 데이터에 적용할수 있는 신경망의 자연스러운 구조라는 것입니다. 과연 그럴까요?

재귀신경망은 확실히 시퀀스나 리스트 형태의 데이터를 처리하는데 이미 사용되고 있습니다! 지난 몇년 동안 음성인식, 언어모델링, 번역, 이미지 캡션과 같은 다양한 문제들에 대해 RNN이 성공적으로 적용되었습니다. 계속해서 Andrej Karpathy의 훌륭한 블로그 게시물인 Reason Neural Networks의 비상식적으로 (좋은) 효과를 살펴보면서, RNN으로 함께 달성할 수 있는 놀라운 업적에 대해서 논의하겠습니다. 실제로 그것들은 진짜로 훌륭히 일을 할 수 있습니다.

이러한 성공의 핵심은 "LSTM 네트워크"를 사용하는 것인데, 이것은 매우 특별한 종류의 재귀적 신경망이며 많은 작업에 대해서 표준 버전의 재귀신경망보다 훨씬 효과적으로 작동합니다. 재귀적 신경망을 기반으로 한 거의 모든 흥미 진진한 결과는 이들과 함께 달성됩니다. 바로 이 에세이에서 살펴볼 LSTM 네트워크입니다.

### 장기적 종속성의 문제(The Problem of Long-Term Dependencies)
RNN의 매력중 한가지는 이전 비디오 프레임을 사용하여 현재 프레임의 이해를 알리는 것처럼 이전의 정보를 현재의 작업에 연결할 수 있다는 생각입니다. 만약 이를 수행할 수 있다면 RNN은 매우 유용할 것이다. 이것이 가능할까요? 그것은 경우에 따라 다릅니다.

때로는 현재의 작업을 처리하기 위해서 단지 최근의 정보만을 살펴봐야 할때도 있습니다. 예를 들어, 이전 단어를 기반으로 다음 단어를 예측하려고 시도하는 언어 모델을 생각해 봅시다. 우리가 "the clouds are in the sky" 라는 문장에서 마지막 단어를 예측하려고 한다면, 우리는 더 이상의 정보를 필요로 하지 않습니다. 다음 단어가 sky가 될 것이란 것은 매우 분명합니다. 그러한 경우, 즉 관련된 정보와 그것을 필요로 하는 장소 사이의 간격이 작은 경우에는, RNN은 과거의 정보를 사용하는 방법을 배울 수 있습니다.

<div style="text-align:center" markdown="1">
![](https://www.dropbox.com/s/ktw35gp24wfob16/RNN-shorttermdepdencies.png?dl=1){:height="200px" .center-image}

**그림.** 단기 종속성의 경우
</div>

그러나, 더 많은 맥락을 필요로 하는 경우들도 있습니다. "I grew up in France... I speak fluent French." 라는 텍스트에서 마지막 단어를 예측하려고 해봅시다. 마지막 단어의 최근 정보는 다음에 오는 단어가 아마도 언어의 이름이라고 제안할 수 있겠지만, 어떤 언어인지로 좁히기 위해서는, 더 뒤로부터 France의 맥락을 필요로 합니다. 연관된 정보와 그것이 필요로 해지는 시점간의 간격이 매우 커지게 되는 상황은 전적으로 가능합니다. 불행히도 그 격차가 커지면 RNN은 정보를 연결하는 법을 배울 수 없게 됩니다.

<div style="text-align:center" markdown="1">
![](https://www.dropbox.com/s/g3v59uu75vwo1td/RNN-longtermdependencies.png?dl=1){:height="200px" .center-image}

**그림.** 장기 종속성의 경우
</div>

이론적으로는 RNN이 이러한 "장기적 의존성"을 절대적으로 처리할 수는 있습니다. 인간이 이러한 형태의 쉬운 문제를 해결하기 위해서 신중히 매개변수를 선택할 수 있기때문입니다. 그러나 슬프게도.. 실질적으로는, RNN은 그러한 장기적 의존성문제를 해결하도록 학습할 수 있을 것 같지는 않습니다. 이 문제는 Hochreiter (1991) [독일]와 Bengio, et al. (1994)에 의해서 깊이 있게 조사되었는데, 그들은 이러한 장기적 의존성을 학습하는 문제가 해결되기 어려운 몇가지의 매우 근본적 이유를 발견하였습니다.

고맙게도, LSTM 네트워크에는 이러한 문제가 없습니다!

### LSTM 네트워크
Long Short Term Memory 네트워크 (일반적으로 "LSTM"이라고 함)는 특별한 종류의 RNN이며 장기 의존성을 학습할 수 있도록 설계되었습니다. 이것은 Hochreiter & Schmidhuber (1997)에 의해 소개되었고, 다음과 같은 업적을 남긴 많은 사람들에 의해서 개선되고 대중화되었습니다. 이들은 다양한 문제에 대해 대단히 잘 작동하며 현재 널리 사용되고 있습니다.

LSTM은 장기 의존성 문제를 피하기 위해 명시적으로 설계되었습니다. 장기적 정보의 기억은 실질적으로 이 네트워크의 기본행동이며 그러므로 어렵게 배울 필요가 없습니다!

모든 재귀적 신경망은 신경망의 반복적인 모듈 체인의 형태를 가집니다. 표준 RNN에서는, 이러한 재귀적으로 반복하는 모듈은 단일의 tanh 계층처럼 같은 매우 간단한 구조를 가집니다.

<div style="text-align:center" markdown="1">
![](https://www.dropbox.com/s/1szbjccvb228ckq/LSTM3-SimpleRNN.png?dl=1){:height="200px" .center-image}

**그림.** 표준 RNN에서의 반복되는 모듈은 싱글 tanh 계층을 포함합니다.
</div>

LSTM 네트워크들도 이러한 체인구조를 가지지만, 그 반복 모듈들의 구조는 상이합니다. 단일의 뉴럴네트워크 구조를 가지는 대신에, 아주 특별한 방식으로 상호작용하는 4개의 계층을 가집니다.

**그림.** The repeating module in an LSTM contains four interacting layers.

무슨 일이 일어나는지에 대한 세부적 사항은 걱정할 필요가 없습니다. 우리는 나중에 LSTM 다이어그램을 단계적으로 살펴보도록 할 것이니까요. 지금은 사용하는 표기법에 익숙해 지도록 노력해 봅시다.

**그림.**

위의 다이어그램에서 각 선은 한 노드의 출력에서 다른 노드의 입력까지 전체 벡터를 전달합니다. 핑크색 원은 벡터 추가와 같은 pointwise 연산을 나타내며, 노란색 상자는 뉴럴네트워크 계층을 학습한 것입니다. 병합되는 선은 연결을 나타내는 반면 분기는 내용이 복사되고 다른 선으로 이동한다는 것을 나타냅니다.

### The Core Idea Behind LSTMs

LSTM의 핵심은 셀 상태이며 그것은 다이어그램의 상단을 가로 지르는 수평선입니다.

셀 상태는 일종의 컨베이어 벨트와 같습니다. 그것은 사소한 선형적 상호작용만을 하면서 체인 전체를 똑바로 따라갑니다. 정보가 변경되지 않고 그대로 전달되는 것은 매우 쉽습니다.


그림.

LSTM 네트워크에는 게이트라고 불리우는 구조에 의해 조심스럽게 조절되는 셀의 상태에 정보를 제거하거나 추가 할 수 있는 기능이 있습니다.

게이트는 선택적으로 정보를 전달할 수 있는 방법입니다. 그것들은 시그모이드 신경망 계층 pointwise 곱셈 연산으로 구성되어 있습니다.

그림.

시그모이드 계층은 0과 1사이의 숫자를 출력함으로써 각 구성요소의 얼마 만큼을 통과시켜야 할지를 기술합니다. 0 값은 "아무 것도 통과시키지 말 것"을 의미하고 1 값은 "모든 것을 통과시킬 것!"을 의미합니다.

LSTM 네트워크에는 셀 상태를 보호하고 제어하기 위한 세 개의 게이트가 있습니다.

### Step-by-Step LSTM Walk Through

LSTM 네트워크의 첫번째 단계는 셀 상태로부터 벗어버릴 정보를 결정하는 것입니다. 이 결정은 망각 게이트 계층이라고 불리는 시그모이드 계층에 의해서 이루어 집니다. 그것은 $$h_{t-1}$$과 $$x_t$$를 보고 셀 상태인 $$C_{t-1}$$에서 각 번에 대해서 00과 11사이의 숫자를 출력합니다. 11은 "완전히 보존하라"는 것을 지시하며 00은 "완전히 이것을 버려라"는 것을 지시합니다.

이전에 출현한 모든 단어들을 바탕으로 다음 단어를 예측하려고 시도하는 언어 모델의 예제로 돌아가 보겠습니다. 그러한 문제에서, 셀 상태에는 현재 대상의 성별이 포함될 수 있으므로 올바른 대명사를 사용할 수 있습니다. 새로운 주어가 보일 때, 우리는 이전 주어의 성을 잊기를 원할 것입니다.

그림

다음 단계는 우리가 셀의 상태로 저장할 새로운 정보가 무엇인지 결정하는 것입니다. 여기에는 두 부분이 있습니다. 먼저 "입력 게이트 계층"이라고 하는 시그모이드 계층이 갱신할 값을 결정합니다. 그 다음, tanh 계층은 상태에 추가될 수 있는 새로운 후보 값 $$\widetilde{C}_t$$ 벡터를 생성합니다. 다음 단계에서는 이 두 요소(무엇을 잊고 무엇을 기억할지에 관한 두 요소)를 결합하여 상태를 업데이트합니다.

우리 언어 모델의 예제에서, 우리는 잊고있는 오래된 것을 대체하기 위해 새로운 주체의 성별을 셀 상태에 추가하려고합니다.

The next step is to decide what new information we’re going to store in the cell state. This has two parts. First, a sigmoid layer called the “input gate layer” decides which values we’ll update. Next, a tanh layer creates a vector of new candidate values, C~tC~t, that could be added to the state. In the next step, we’ll combine these two to create an update to the state.

In the example of our language model, we’d want to add the gender of the new subject to the cell state, to replace the old one we’re forgetting.

그림.

It’s now time to update the old cell state, Ct−1Ct−1, into the new cell state CtCt. The previous steps already decided what to do, we just need to actually do it.

We multiply the old state by ftft, forgetting the things we decided to forget earlier. Then we add it∗C~tit∗C~t. This is the new candidate values, scaled by how much we decided to update each state value.

In the case of the language model, this is where we’d actually drop the information about the old subject’s gender and add the new information, as we decided in the previous steps.

그림.

Finally, we need to decide what we’re going to output. This output will be based on our cell state, but will be a filtered version. First, we run a sigmoid layer which decides what parts of the cell state we’re going to output. Then, we put the cell state through tanhtanh (to push the values to be between −1−1 and 11) and multiply it by the output of the sigmoid gate, so that we only output the parts we decided to.

For the language model example, since it just saw a subject, it might want to output information relevant to a verb, in case that’s what is coming next. For example, it might output whether the subject is singular or plural, so that we know what form a verb should be conjugated into if that’s what follows next.

그림.

### Variants on Long Short Term Memory
What I’ve described so far is a pretty normal LSTM. But not all LSTMs are the same as the above. In fact, it seems like almost every paper involving LSTMs uses a slightly different version. The differences are minor, but it’s worth mentioning some of them.

One popular LSTM variant, introduced by Gers & Schmidhuber (2000), is adding “peephole connections.” This means that we let the gate layers look at the cell state.

그림.

The above diagram adds peepholes to all the gates, but many papers will give some peepholes and not others.

Another variation is to use coupled forget and input gates. Instead of separately deciding what to forget and what we should add new information to, we make those decisions together. We only forget when we’re going to input something in its place. We only input new values to the state when we forget something older.

그림.

A slightly more dramatic variation on the LSTM is the Gated Recurrent Unit, or GRU, introduced by Cho, et al. (2014). It combines the forget and input gates into a single “update gate.” It also merges the cell state and hidden state, and makes some other changes. The resulting model is simpler than standard LSTM models, and has been growing increasingly popular.

그림.

These are only a few of the most notable LSTM variants. There are lots of others, like Depth Gated RNNs by Yao, et al. (2015). There’s also some completely different approach to tackling long-term dependencies, like Clockwork RNNs by Koutnik, et al. (2014).

Which of these variants is best? Do the differences matter? Greff, et al. (2015) do a nice comparison of popular variants, finding that they’re all about the same. Jozefowicz, et al. (2015) tested more than ten thousand RNN architectures, finding some that worked better than LSTMs on certain tasks.

### Conclusion

Earlier, I mentioned the remarkable results people are achieving with RNNs. Essentially all of these are achieved using LSTMs. They really work a lot better for most tasks!

Written down as a set of equations, LSTMs look pretty intimidating. Hopefully, walking through them step by step in this essay has made them a bit more approachable.

LSTMs were a big step in what we can accomplish with RNNs. It’s natural to wonder: is there another big step? A common opinion among researchers is: “Yes! There is a next step and it’s attention!” The idea is to let every step of an RNN pick information to look at from some larger collection of information. For example, if you are using an RNN to create a caption describing an image, it might pick a part of the image to look at for every word it outputs. In fact, Xu, et al. (2015) do exactly this – it might be a fun starting point if you want to explore attention! There’s been a number of really exciting results using attention, and it seems like a lot more are around the corner…

Attention isn’t the only exciting thread in RNN research. For example, Grid LSTMs by Kalchbrenner, et al. (2015) seem extremely promising. Work using RNNs in generative models – such as Gregor, et al. (2015), Chung, et al. (2015), or Bayer & Osendorfer (2015) – also seems very interesting. The last few years have been an exciting time for recurrent neural networks, and the coming ones promise to only be more so!

### Acknowledgments

I’m grateful to a number of people for helping me better understand LSTMs, commenting on the visualizations, and providing feedback on this post.

I’m very grateful to my colleagues at Google for their helpful feedback, especially Oriol Vinyals, Greg Corrado, Jon Shlens, Luke Vilnis, and Ilya Sutskever. I’m also thankful to many other friends and colleagues for taking the time to help me, including Dario Amodei, and Jacob Steinhardt. I’m especially thankful to Kyunghyun Cho for extremely thoughtful correspondence about my diagrams.

Before this post, I practiced explaining LSTMs during two seminar series I taught on neural networks. Thanks to everyone who participated in those for their patience with me, and for their feedback.



(진행중)
