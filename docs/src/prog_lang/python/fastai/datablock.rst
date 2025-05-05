DataBlock: shape of data
======================================

Not until calling `DataBlock.dataloaders` then DataBlock is
actually related to any data.

There are several components in a DataBlock:

- input and target blocks
- how to get items when supplied path
- how to get label when supplied path
- what is the splitter for training and validation
- any transform on the item

These make it to be like this:

.. code-block:: python

    # in the oxford-iiit-pet, there is a convention that 
    # cat images are starting with capitalized name
    # dog images are starting with un-capitalized name
    get_label = lambda fname: "cat" if fname.name[0].isupper() else "dog"

    dblock = DataBlock(
        blocks    = (ImageBlock, CategoryBlock),
        get_items = get_image_files,
        get_y     = get_label,
        splitter  = RandomSplitter(),
        item_tfms = Resize(224)
    )

.. note:: A way to know data within URLs is by using DataBlock.summary(unstart_data(URLs.XXX))

    It will tell you more about the dataset and how it will be handled.

MNIST Example
------------------------------

MNIST is a dataset of hand-written digits from 0 to 9. 
We can very easily load it in the data block API by answering the following questions:

- what are the types of our inputs and targets? Black and white images and labels.
- where is the data? In subfolders.
- how do we know if a sample is in the training or the validation set? By looking at the grandparent folder.
- how do we know the label of an image? By looking at the parent folder.
- In terms of the API, those answers translate like this:

.. code-block:: python

    mnist = DataBlock(
        blocks=(ImageBlock(cls=PILImageBW), CategoryBlock), 
        get_items=get_image_files, 
        splitter=GrandparentSplitter(),
        get_y=parent_label
    )
