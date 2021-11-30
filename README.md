# IFDD
Few-shot NEU-DET (FS-ND)  
This is the dataset used in our paper Few-Shot Steel Surface Defect Detection (will be published soon). The dataset is reconstructed from the famous [NEU-DET](https://ieeexplore.ieee.org/abstract/document/8709818) dataset and designed specially for few-shot defect detection.  
The FS-ND can be downloaded [here](https://drive.google.com/drive/folders/1Somtykp_DwqGTe5by9PEfPDxPqYRFu-L)
If you use the FS-ND, please cite our paper:  
@article{wang2021few,  
  title={Few-Shot Steel Surface Defect Detection},  
  author={Wang, Haohan and Li, Zhuoling and Wang, Haoqian},  
  journal={IEEE Transactions on Instrumentation and Measurement},  
  year={2021},  
  publisher={IEEE}  
}

## How to use FS-ND?
There are 4 zip files in the link above: **NEU-DET-METATRAIN**, which is used for meta-training (base training), and **5shot1-100**, **10shot1-100** and **30shot1-100**, which are used for meta-testing (few-shot fine-tuning). For k-shot experiment, you should first train your model with **NEU-DET-METATRAIN**, then evaluate it with the corresponding **kshot1-100**, where k=5,10,30.  
There are 100 data folder in the **kshot1-100.zip**: **kshot1**, **kshot2**...**kshot100**. Each **kshoti** (k=5,10,30 and i = 1,2,3...100) folder has the same structure:  

**kshoti  
├── annotations &emsp;&emsp;# two json files, the annoations for train2017 and val2017  
├── train2017 &emsp;&emsp;&nbsp;&nbsp;&nbsp;&nbsp;# support examples (3*k images)  
├── val2017 &emsp;&emsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;# query images, this folder stays same when k or i changes    
├── trainval.txt  &emsp;&emsp;&nbsp;# intermediate result when constructing data, no attention needed  
├── test.txt &emsp;&emsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;# intermediate result when constructing data, no attention needed**  
The **kshoti** has the same structure as the famous **COCO** dataset, so you can use the same dataloader with minor adjustments. The two txt file can also be useful if you would like to further analysis the data.   
The **NEU-DET-METATRAIN** shares the same structure with **kshoti**, where its **train2017** contains more images and its **val2017** can be utilized to evaluate the pre-trained model. However, the results on **NEU-DET-METATRAIN/val2017** are just intermediate results and do not reflect the few-shot performance.  

## Why we reconstruct NEU-DET?
Although few-shot defect detection technique is quite valuable due to the scarcity of industrial data, there is no publicly available few-shot defect detection dataset. We can utilize the existing NEU-DET to evaluate few-shot detection tasks, but it actually introduces much randomness.  
First, the different training and testing split has an unpredictable effect, even the same model can perform differently in different works.  
Second, the sample of support examples makes the results unstable, as the quality of each training image differs a lot.  
To bridge this gap, we reconstruct NEU-DET into the few-shot form, namely few-shot NEU-DET (FS-ND). 

## How we make FS-ND?
we fix the partition of training and testing data, and for each k-shot setting (k=5,10,30), we sample 100 groups support examples to reduce the randomness.  
Specifially, three types of defects (inclusion, rolled-in scales and scratches) are utilized as the base data for training, and the others (crazing, patches and pitted surface) are reserved for testing.  
For more details about how the NEU-DET is reconstructed, please refer to our paper (coming soon)  
