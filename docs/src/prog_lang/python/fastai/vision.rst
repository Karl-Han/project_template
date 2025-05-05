Vision Models
===============================

Beginner with Learner to Finetune
---------------------------------------

Refer to `Computer Vision Intro <https://docs.fast.ai/tutorial.vision.html>`_,
it is just finetune a pretrained model with Learner and apply it in the new problem.

Though it is confusing with lots of layers of abstraction, it is important to 
get the idea that the general way is to:

1. get the root folder path of the dataset
2. define the shape/datablock is like, refer to :doc:`/prog_lang/python/fastai/datablock`
3. combine the paths and datablocks to dataloader, which will load the data
4. combine the dataloader and the actual model with parameters to be learner
5. fit the learner if you are training the new model, and fine tune if with existing