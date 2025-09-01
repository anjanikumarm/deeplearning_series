# RNN vs NN explained visually with an example numerical dataset

For tasks involving sequences, a Recurrent Neural Network (RNN) excels where a traditional Neural Network (NN) fails because of a key difference: RNNs have an internal "memory". A conventional NN processes each input independently, assuming no prior context, while an RNN's output depends on previous steps in the sequence. \[[1](https://www.analyticsvidhya.com/blog/2022/03/a-brief-overview-of-recurrent-neural-networks-rnn/), [2](https://www.e2enetworks.com/blog/ann-vs-cnn-vs-rnn-exploring-the-neural-networks-in-ai)\]

Example: Predicting a numerical sequence

Let's use a simple dataset to predict the next number in a sequence based on the previous two: .

The dataset

**Our goal is to predict the third number from the first two.**

| Previous 2 numbers (Inputs) | Next number (Output) |
| --- | --- |
| —   | —   |
| --- | --- |
| —   | —   |
| --- | --- |
| —   | —   |
| --- | --- |
| —   | —   |
| --- | --- |

How a traditional Neural Network (NN) works

A traditional NN treats each input-output pair as an independent event. It cannot learn the underlying relationship between a sequence of inputs. \[[3](https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network), [4](https://medium.com/@poudelsushmita878/recurrent-neural-network-rnn-architecture-explained-1d69560541ef), [5](https://www.mdpi.com/1996-1073/15/18/6745#:~:text=In%20traditional%20neural%20networks%2C%20signals%20are%20not,relationship%20or%20sequence%20of%20the%20input%20signal.), [6](https://search.proquest.com/openview/5fcdaa7df6dc649e1a9614fdbcb6858a/1?pq-origsite=gscholar&cbl=2037347#:~:text=Since%20FCNNs%20cannot%20share%20features%20between%20different,back%20and%20forth%20in%20time%20or%20space.)\]

**NN architecture for the example dataset**

- **Input Layer:** Two neurons, one for each of the previous two numbers.
- **Hidden Layers:** One or more layers to learn the mapping from inputs to the output.
- **Output Layer:** One neuron to predict the next number. \[[7](https://www.researchgate.net/figure/shows-the-NN-example-that-has-an-input-layer-with-n-neurons-a-hidden-layer-with-two_fig4_355025116#:~:text=The%20input%20layer%20is%20composed%20of%20neurons,of%20the%20neurons%20of%20the%20previous%20layer.), [8](https://dev.to/farshed/building-a-neural-network-in-rust-from-scratch-5bm1#:~:text=The%20neural%20network%20we're%20building%20looks%20like,that%20it%20doesn't%20have%20any%20hidden%20layers.), [9](https://developers.google.com/machine-learning/crash-course/neural-networks/nodes-hidden-layers#:~:text=Adding%20layers%20to%20the%20network%0A%0ABut%20what%20if,nodes%20in%20these%20layers%20are%20called%20neurons.), [10](https://medium.com/@haein.park1907/from-a-simple-neural-network-to-the-llm-basic-structure-of-the-neural-network-d9c277283855#:~:text=Hidden%20Layer:%20Hidden%20layers%20are%20simply%20the,help%20the%20NN%20learn%20and%20make%20prediction.), [11](https://www.degruyterbrill.com/document/doi/10.1515/jisys-2023-0318/html#:~:text=In%20neural%20networks%2C%20the%20output%20layer%20is,%281%20represents%20risk%2C%200%20represents%20no%20risk%29.)\]

**Visualizing the process with the NN**Here's how a traditional NN would learn from the sequence data. Notice that each input is processed separately. The network for predicting is completely independent of the network that predicted . \[[12](https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network), [13](https://www.ibm.com/think/topics/recurrent-neural-networks), [14](https://www.naukri.com/code360/library/recurrent-neural-network-intro#:~:text=In%20a%20standard%20neural%20network%2C%20inputs%20are,from%20one%20time%20step%20to%20the%20next.)\]

**Training step 1**

- **Inputs:**
- **Network:** Processes and
- **Predicted output:** (If trained correctly)

**Training step 2**

- **Inputs:**
- **Network:** Processes and
- **Predicted output:**

**Training step 3**

- **Inputs:**
- **Network:** Processes and
- **Predicted output:**

**Limitation:** If you provide new, unseen input like , the NN will make a prediction based purely on the relationship, not the broader pattern of the original sequence. It has no context of the sequence's history.

How a Recurrent Neural Network (RNN) works

An RNN is designed for sequential data because it passes information from one step to the next. This creates an internal "memory," or **hidden state**, that influences the current output. The network performs the same task for every element of the sequence. \[[1](https://www.analyticsvidhya.com/blog/2022/03/a-brief-overview-of-recurrent-neural-networks-rnn/), [15](https://purnasaigudikandula.medium.com/recurrent-neural-networks-and-lstm-explained-7f51c7f6bbb9), [16](https://www.springboard.com/blog/data-science/rnn-vs-cnn/), [17](https://www.geeksforgeeks.org/machine-learning/introduction-to-recurrent-neural-network/)\]

**RNN architecture for the example datasetAn RNN is essentially a single network structure that is unrolled over time.**

- **Recurrent connection:** A feedback loop passes the output of the hidden layer at one time step as an input to the hidden layer at the next time step.
- **Shared parameters:** The network uses the same weights and bias parameters across all time steps, reducing model complexity. \[[3](https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network), [17](https://www.geeksforgeeks.org/machine-learning/introduction-to-recurrent-neural-network/), [18](https://www.e2enetworks.com/blog/ann-vs-cnn-vs-rnn-exploring-the-neural-networks-in-ai), [19](https://medium.com/@prashantgupta17/recurrent-neural-networks-in-machine-learning-759a943fa759#:~:text=In%20other%20words%2C%20the%20output%20or%20hidden,from%20the%20past%20into%20the%20present.%20where:), [20](https://www.naukri.com/code360/library/recurrent-neural-network-intro#:~:text=However%2C%20in%20an%20RNN%2C%20each%20neuron%20in,time%20steps%29%20to%20influence%20the%20current%20output.)\]

**Visualizing the process with the RNN**Here is a step-by-step breakdown of how an unrolled RNN processes the sequence. \[[21](https://www.cudocompute.com/topics/neural-networks/introduction-to-recurrent-neural-networks-rnns#:~:text=To%20better%20visualize%20how%20an%20RNN%20processes,passed%20from%20one%20layer%20to%20the%20next.)\]

**Training step 1: Process**

- **Input:**
- **Hidden state:** The initial state is typically a vector of zeros.
- **Process:** The network takes the input and the initial hidden state to produce a new hidden state and an output.
- **Output:** Not used for this step. \[[22](https://5ly.co/blog/recurrent-neural-networks-mechanics/#:~:text=At%20each%20time%20step%2C%20the%20RNN%20receives,that%20retains%20information%20from%20previous%20time%20steps.), [23](https://www.analyticsvidhya.com/blog/2023/05/top-interview-questions-for-rnn/#:~:text=The%20architecture%20of%20an%20RNN%20consists%20of,an%20output%20and%20a%20new%20hidden%20state.), [24](https://link.springer.com/article/10.1007/s00521-019-04695-8#:~:text=In%20a%20BPNN%2C%20generally%2C%20there%20is%20an,processing%20layer%20is%20called%20the%20output%20layer.), [25](https://www.sciencedirect.com/science/article/pii/B9780323983525000094#:~:text=The%20reason%20to%20develop%20the%20RNN%20is,output%20has%20no%20relation%20with%20previous%20output.)\]

**Training step 2: Process**

- **Input:**
- **Hidden state:** The network uses the hidden state from the previous step (from processing ).
- **Process:** The network combines the input with the previous hidden state to produce a new hidden state and an output.
- **Predicted output:** (based on the context of and ). \[[26](https://jpt.spe.org/twa/lstm-for-production-part-1#:~:text=For%20instance%2C%20if%20the%20input%20is%2010%2Dtime,%28%F0%9D%91%8E%20%3C%F0%9D%91%A1%3E%29%20and%20a%20prediction%20%28y%20%3C%F0%9D%91%A1%3E%29.)\]

**Training step 3: Process**

- **Input:**
- **Hidden state:** The network uses the hidden state from the previous step (from processing and ).
- **Process:** The network combines the input with the previous hidden state.
- **Predicted output:** . \[[27](https://link.springer.com/article/10.1007/s11227-022-04970-x#:~:text=1%2C%20RNN%20is%20the%20computation%20of%20hidden,when%20we%20need%20more%20and%20further%20information.), [28](https://search.proquest.com/openview/1125c6e722bdba6487248aa53ed17671/1?pq-origsite=gscholar&cbl=5444811)\]

**Key takeaway: RNN's "memory"**The RNN's hidden state effectively captures the "storyline" of the sequence, allowing it to understand the pattern. When it sees in step 3, it remembers that it came after and , providing crucial context for predicting . \[[29](https://medium.com/@muskanmarghani13/recurrent-neural-networks-rnns-explained-architecture-applications-and-limitations-2a2c8a40ca57)\]

**Summary of differences**

| Feature \[[1](https://www.analyticsvidhya.com/blog/2022/03/a-brief-overview-of-recurrent-neural-networks-rnn/), [3](https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network), [12](https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network), [15](https://purnasaigudikandula.medium.com/recurrent-neural-networks-and-lstm-explained-7f51c7f6bbb9), [16](https://www.springboard.com/blog/data-science/rnn-vs-cnn/), [17](https://www.geeksforgeeks.org/machine-learning/introduction-to-recurrent-neural-network/), [30](https://insights.daffodilsw.com/blog/cnn-vs-rnn-whats-the-difference), [31](https://www.geeksforgeeks.org/machine-learning/introduction-to-recurrent-neural-network/), [32](https://learninglabb.com/difference-between-cnn-and-rnn/#:~:text=What%20is%20RNN%20%28Recurrent%20Neural%20Network%29?%20RNN%2C,for%20tasks%20that%20involve%20patterns%20over%20time.)\] | Traditional Neural Network (NN) | Recurrent Neural Network (RNN) |
| --- | --- | --- |
| **Data type** | Independent data points, assuming inputs and outputs are not related to each other. | Sequential data, where the order of elements is important, such as time series. |
| --- | --- | --- |
| **Architecture** | A feedforward structure where information flows in one direction, from input to output. | Contains a feedback loop, allowing information to persist and cycle back into the network. |
| --- | --- | --- |
| **Memory** | Has no internal memory of previous inputs. | Contains an internal hidden state that serves as a memory of past inputs. |
| --- | --- | --- |
| **Parameter usage** | Uses a separate set of weights for each layer. | Shares the same weight matrices across all time steps. |
| --- | --- | --- |
| **Use case** | Image classification, tabular data analysis, and other tasks without sequential dependencies. | Natural Language Processing (NLP), time series prediction, speech recognition, and any other task where context is vital. |
| --- | --- | --- |

_AI responses may include mistakes._

\[1\] <https://www.analyticsvidhya.com/blog/2022/03/a-brief-overview-of-recurrent-neural-networks-rnn/>

\[2\] <https://www.e2enetworks.com/blog/ann-vs-cnn-vs-rnn-exploring-the-neural-networks-in-ai>

\[3\] <https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network>

\[4\] <https://medium.com/@poudelsushmita878/recurrent-neural-network-rnn-architecture-explained-1d69560541ef>

\[5\] [https://www.mdpi.com/1996-1073/15/18/6745](https://www.mdpi.com/1996-1073/15/18/6745#:~:text=In%20traditional%20neural%20networks%2C%20signals%20are%20not,relationship%20or%20sequence%20of%20the%20input%20signal.)

\[6\] [https://search.proquest.com/openview/5fcdaa7df6dc649e1a9614fdbcb6858a/1?pq-origsite=gscholar&cbl=2037347](https://search.proquest.com/openview/5fcdaa7df6dc649e1a9614fdbcb6858a/1?pq-origsite=gscholar&cbl=2037347#:~:text=Since%20FCNNs%20cannot%20share%20features%20between%20different,back%20and%20forth%20in%20time%20or%20space.)

\[7\] [https://www.researchgate.net/figure/shows-the-NN-example-that-has-an-input-layer-with-n-neurons-a-hidden-layer-with-two_fig4_355025116](https://www.researchgate.net/figure/shows-the-NN-example-that-has-an-input-layer-with-n-neurons-a-hidden-layer-with-two_fig4_355025116#:~:text=The%20input%20layer%20is%20composed%20of%20neurons,of%20the%20neurons%20of%20the%20previous%20layer.)

\[8\] [https://dev.to/farshed/building-a-neural-network-in-rust-from-scratch-5bm1](https://dev.to/farshed/building-a-neural-network-in-rust-from-scratch-5bm1#:~:text=The%20neural%20network%20we're%20building%20looks%20like,that%20it%20doesn't%20have%20any%20hidden%20layers.)

\[9\] [https://developers.google.com/machine-learning/crash-course/neural-networks/nodes-hidden-layers](https://developers.google.com/machine-learning/crash-course/neural-networks/nodes-hidden-layers#:~:text=Adding%20layers%20to%20the%20network%0A%0ABut%20what%20if,nodes%20in%20these%20layers%20are%20called%20neurons.)

\[10\] [https://medium.com/@haein.park1907/from-a-simple-neural-network-to-the-llm-basic-structure-of-the-neural-network-d9c277283855](https://medium.com/@haein.park1907/from-a-simple-neural-network-to-the-llm-basic-structure-of-the-neural-network-d9c277283855#:~:text=Hidden%20Layer:%20Hidden%20layers%20are%20simply%20the,help%20the%20NN%20learn%20and%20make%20prediction.)

\[11\] [https://www.degruyterbrill.com/document/doi/10.1515/jisys-2023-0318/html](https://www.degruyterbrill.com/document/doi/10.1515/jisys-2023-0318/html#:~:text=In%20neural%20networks%2C%20the%20output%20layer%20is,%281%20represents%20risk%2C%200%20represents%20no%20risk%29.)

\[12\] <https://www.datacamp.com/tutorial/tutorial-for-recurrent-neural-network>

\[13\] <https://www.ibm.com/think/topics/recurrent-neural-networks>

\[14\] [https://www.naukri.com/code360/library/recurrent-neural-network-intro](https://www.naukri.com/code360/library/recurrent-neural-network-intro#:~:text=In%20a%20standard%20neural%20network%2C%20inputs%20are,from%20one%20time%20step%20to%20the%20next.)

\[15\] <https://purnasaigudikandula.medium.com/recurrent-neural-networks-and-lstm-explained-7f51c7f6bbb9>

\[16\] <https://www.springboard.com/blog/data-science/rnn-vs-cnn/>

\[17\] <https://www.geeksforgeeks.org/machine-learning/introduction-to-recurrent-neural-network/>

\[18\] <https://www.e2enetworks.com/blog/ann-vs-cnn-vs-rnn-exploring-the-neural-networks-in-ai>

\[19\] [https://medium.com/@prashantgupta17/recurrent-neural-networks-in-machine-learning-759a943fa759](https://medium.com/@prashantgupta17/recurrent-neural-networks-in-machine-learning-759a943fa759#:~:text=In%20other%20words%2C%20the%20output%20or%20hidden,from%20the%20past%20into%20the%20present.%20where:)

\[20\] [https://www.naukri.com/code360/library/recurrent-neural-network-intro](https://www.naukri.com/code360/library/recurrent-neural-network-intro#:~:text=However%2C%20in%20an%20RNN%2C%20each%20neuron%20in,time%20steps%29%20to%20influence%20the%20current%20output.)

\[21\] [https://www.cudocompute.com/topics/neural-networks/introduction-to-recurrent-neural-networks-rnns](https://www.cudocompute.com/topics/neural-networks/introduction-to-recurrent-neural-networks-rnns#:~:text=To%20better%20visualize%20how%20an%20RNN%20processes,passed%20from%20one%20layer%20to%20the%20next.)

\[22\] [https://5ly.co/blog/recurrent-neural-networks-mechanics/](https://5ly.co/blog/recurrent-neural-networks-mechanics/#:~:text=At%20each%20time%20step%2C%20the%20RNN%20receives,that%20retains%20information%20from%20previous%20time%20steps.)

\[23\] [https://www.analyticsvidhya.com/blog/2023/05/top-interview-questions-for-rnn/](https://www.analyticsvidhya.com/blog/2023/05/top-interview-questions-for-rnn/#:~:text=The%20architecture%20of%20an%20RNN%20consists%20of,an%20output%20and%20a%20new%20hidden%20state.)

\[24\] [https://link.springer.com/article/10.1007/s00521-019-04695-8](https://link.springer.com/article/10.1007/s00521-019-04695-8#:~:text=In%20a%20BPNN%2C%20generally%2C%20there%20is%20an,processing%20layer%20is%20called%20the%20output%20layer.)

\[25\] [https://www.sciencedirect.com/science/article/pii/B9780323983525000094](https://www.sciencedirect.com/science/article/pii/B9780323983525000094#:~:text=The%20reason%20to%20develop%20the%20RNN%20is,output%20has%20no%20relation%20with%20previous%20output.)

\[26\] [https://jpt.spe.org/twa/lstm-for-production-part-1](https://jpt.spe.org/twa/lstm-for-production-part-1#:~:text=For%20instance%2C%20if%20the%20input%20is%2010%2Dtime,%28%F0%9D%91%8E%20%3C%F0%9D%91%A1%3E%29%20and%20a%20prediction%20%28y%20%3C%F0%9D%91%A1%3E%29.)

\[27\] [https://link.springer.com/article/10.1007/s11227-022-04970-x](https://link.springer.com/article/10.1007/s11227-022-04970-x#:~:text=1%2C%20RNN%20is%20the%20computation%20of%20hidden,when%20we%20need%20more%20and%20further%20information.)

\[28\] <https://search.proquest.com/openview/1125c6e722bdba6487248aa53ed17671/1?pq-origsite=gscholar&cbl=5444811>

\[29\] <https://medium.com/@muskanmarghani13/recurrent-neural-networks-rnns-explained-architecture-applications-and-limitations-2a2c8a40ca57>

\[30\] <https://insights.daffodilsw.com/blog/cnn-vs-rnn-whats-the-difference>

\[31\] <https://www.geeksforgeeks.org/machine-learning/introduction-to-recurrent-neural-network/>

\[32\] [https://learninglabb.com/difference-between-cnn-and-rnn/](https://learninglabb.com/difference-between-cnn-and-rnn/#:~:text=What%20is%20RNN%20%28Recurrent%20Neural%20Network%29?%20RNN%2C,for%20tasks%20that%20involve%20patterns%20over%20time.)
