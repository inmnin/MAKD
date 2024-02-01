# MAKD
We provide a pytorch implementation of the MAKD method.

# For the data we used:
All the datasets we have cleaned and segmented are uploaded in this project and users can find them in Data.

# For the environment of the experiment:
We saved the environment configurations used in our experiments in the requirements.txt.

We record the configuration of the devices we used in our experiment as follows for users' reference: RTX 4090(24GB) * 1,12 vCPU Intel(R) Xeon(R) Platinum 8352V CPU @ 2.10GHz. 
Our experiments were done using jupter, if you want to use jupter for your experiments, please create a .ipynb file in the root directory and copy all the contents of main.py or finetune_teacher.py into it and run this ipynb file.

After configuring the environment, experiment with our MAKD method by following two steps

# 1. Fine-tune the teacher model on different datasets:
The fine-tuned teacher model weights for different datasets are expected to be stored in different folders of Teacher_Model. 

If you wish to use the weights we provide, please download https://userscloud.com/fdl7079jlfk7, and then replace the original **Teacher_Model** folder with the unzipped **Teacher_Model** folder **(We recommend this approach)**. 

If you wish to fine-tune the teacher model by yourself, the base parameters used for the teacher model are from  https://userscloud.com/v8bov5yf887d (you can also down it from https://huggingface.co/bert-base-chinese/tree/main, they are the same). After downloading, put the model weights in the Pretrained_BERT folder . Then you need to set train_set_type in finetune_teacher.py to which dataset you want to fine-tune. After setting the parameters, you can run finetune_teacher.py. The teacher's weights fine-tuned for a particular dataset will be saved in the corresponding folder Teacher_Model/xxx_Model/(xxx means data_set_type).
```
    #On which dataset to fine-tune the teacher. 
    #The train_type can be taken as movie, data4, takeaways, shopping or hotel
    data_set_type = "movie"
```

After doing the above, you can start running the MAKD method.

# 2. run MAKD method in main.py:
In experimenting with the MAKD method, please change **train_type** to **"makd"** (or other methods of comparison), and **data_set_type** to the corresponding dataset name (movie,takeaways,data4,shopping or hotel) in main.py. Then set the epochs as **15**, and set the **ALPHA** on different datasets to the best parameters we provided: 
|movie|takeaways|data4|shopping|hotel|
|:---|:---|:---|:---|:---|
|5|3000|1|2.5|0.00003|
```
    EPOCHS = 15

    #ALPHA is the loss weight corresponding to the MAKD loss in the MAKD method
    ALPHA = 5
    
    #The train_type can be one of the following:   makd, pkd_skip, kd, baseline, tiny, minlmv1, or minlmv2
    train_type = "makd"

    #The datasets are of the following types:    hotel, shopping, takeaways, movie, data4
    data_set_type = "movie"
```
After setting these parameters, you can just run main.py. Users can refer to the average of the accuracy of the predictions of the last 5 training rounds of experiments on the test set (that is, the accuracy that will be printed at runtime). 

