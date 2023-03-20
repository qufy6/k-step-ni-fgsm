# k-step-ni-fgsm
Some improvements on ni-fgsm

The core idea of our algorithm is to use the gradient of k steps forward in a round, make a linear accumulation, and then use this strong forward-looking combined gradient to update the attack image in the next round.

But since here the derivative of x t nes i+1 is needed at each calculation of G t nes i+1, it will also include the derivative operation on G t nes i. at the ith operation, it will iteratively find i derivatives of x adv, so that finding higher-order derivatives consumes a lot of arithmetic power, and also they do not have much impact on the results as higher-order small quantities, so we did simplification to save arithmetic power and improve the efficiency of the operation without affecting the accuracy of the calculation.

![Image text](https://github.com/qufy6/k-step-ni-fgsm/blob/main/a.png)

Here is our proposed simplified algorithm: Simple K-STEP Nesterov Iterative Fast Gradient Sign Method , when solving for x t nes i, we use Gt adv instead, which is equivalent to directly rounding off the higher order derivatives, thus reducing the burden of each operation.

![Image text](https://github.com/qufy6/k-step-ni-fgsm/blob/main/b.png)

The adversarial examples are crafted on Inc-v3 using mi-fgsm, ni,-fgsm, k-ni-fgsm, k-si-ni-fgsm with different k. and the inception_v3 is the white-box model being attacked.

In order to choose a more suitable k, we tried different k. Among them, when k=4 and its subsequent values, if the latter β weight is adjusted to be larger, there will be poor performance on some attacks of the anti-attack training model, and there is no significant improvement in other attack cases. Therefore, we set the most suitable k to 3 initially to reduce the number of operations and ensure that all model attacks are optimal. 

![Image text](https://github.com/qufy6/k-step-ni-fgsm/blob/main/c.png)

The adversarial examples are crafted on Inc-v3 using mi-fgsm, ni,-fgsm, k-ni-fgsm, k-si-ni-fgsm with different k. and the inception_v3 is the white-box model being attacked.

In order to choose a more suitable k, we tried different k. Among them, when k=4 and its subsequent values, if the latter β weight is adjusted to be larger, there will be poor performance on some attacks of the anti-attack training model, and there is no significant improvement in other attack cases. Therefore, we set the most suitable k to 3 initially to reduce the number of operations and ensure that all model attacks are optimal. 

![Image text](https://github.com/qufy6/k-step-ni-fgsm/blob/main/d.png)

# RUN
First download the dataset and make files: dev_data, models, nets like reference code.
Then run 'entry.py' and the testing result is in 'nohup.out'.(sure, you can cover it.)

Reference: https://github.com/JHL-HUST/SI-NI-FGSM

