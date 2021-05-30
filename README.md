# hack-q-thon_team27
Q-munity Hackqthon 30 May 2021 <br>
Team members: Jun Wei Chow, Hyun Jin Kim, Timsina Ashok, Rifatul Islam Himel <br>

This repo presents the first mini project for team 27:<br>
Using Machine Learning method to determine output of circuit based on altering $Rx, Ry$ and $Rz$ gate angles<br>

### Technical Discussion

After trying many different models and failing a lot (ipynb files in "deprecated" folder), there are two "successful" models. 

One is using supervised learning (which is actually not too successful based on the training loss) which first create a dataset by randomly assigning values to the $Rx, Ry$ and $Rz$ gates and obtain the counts for each and every available output (by passing them to a qasm_simulator). Then, we construct the dataset containing the values for the counts, with NULL being replaced with 0, and also several targets corresponding to the inner values of $Rx, Ry$ and $Rz$ in several columns depending on how many gates are there (how many degree of freedoms and hence how many values to predict). 

However this method poses a difficulty. Especially with small number of qubits, there are less columns (features) that could be used for training than the columns required to predict. For more information please check out the Jupyter Notebook. 

Second model acts on the failed model of GAN: to change the idea from using GAN which cannot be done due to non-differentiable gradient through qiskit Circuit (or perhaps insufficient skills as a reason) to something that does not rely on requirement for backpropagate through qiskit Circuit, that is, using reinforcement learning. Thanks to the website cited in the jupyter notebook (please refer), we are able to built an environment based on qiskit Circuit and construct reinforcement learning on it. How well this performs, based on the score, not extremely well although overall it gives positive results (might as well be negative depending on how scores/reward are being associated to the model, which is not tuned to its best due to time constraint and understanding difficulty) with some spikes towards extreme positive and extreme negative (much larger than baseline NOT infinity peaks). 

Also, it has not been used to do model.predict as with insufficient skills and perhaps lack of tutorial online on how to use model.predict with reinforcement learning model without looking at the interactive screen while it train to tell it got better. Hence, we will stick to the score. 

### Usage

Perhaps there are times where you would want a certain Gate in a certain library that is, say, available in Qiskit but not available in Amazon Braket. Then, there are originally two ways of transpiling it. First, use the Qiskit Transpiler to transpile the Gate (e.g. MCX Gate) into certain available gates in Braket, then insert each and every one of the gates into Braket. Say, if you have 4000 Gates, then slowly create each and every gate back in Braket. Several days later you will be complete. 

Second method is to use pytket. They offers transpiling to and from Braket, to and from Qiskit. Then this method is more efficient compared to the above method. Although, there are certainly some restrictions in what gates are supported for transpiling towards and from pytket. 

Then we offer another method, of constructing a set of Gates, and use ML to tune the output such that it gives what we would like. This means using a set of gates to re-create the output we want and instead of inserting a giant transpiled circuit, we could just insert this smaller set of Gates to replace the single complex Gate. This makes quantum programmer life easier if they could make available in every single library, especially with tuned rotational values. 

There are further improvements that could be done since some real quantum computer might support controlled $Rx, Ry$ and $Rz$ gates in the future. 

This would also allow us to create circuits that gives us targeted output. If someone only knows the output without knowing which gate and their combination will give the output, they could use this "tuner" to tune the gate to their desired state. The problem will be defined by the user and together with the more popular reinforcement learning methods on placing gates at certain qubits for tuning in some research (no links here because cannot remember where it is seen), to create a result-driven circuit. 

### Inspiration

Thanks to Amira Abbas from this video: https://www.youtube.com/watch?v=r6lZDlNU2JU 

### Miscellaneous

The link to the github repo of second mini project: https://github.com/hjk068/team27_project2_object_recognition
