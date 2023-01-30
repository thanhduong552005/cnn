# cnn
cnn github

import torch
import torch.optim as optim
from PIL import Image, ImageDraw, ImageFont
import torchvision.transforms as transforms
import numpy as np
import json
import requests
import matplotlib.pyplot as plt
import warnings
warnings.filterwarnings('ignore')
device = torch.device("cuda") if torch.cuda.is_available() else torch.device("cpu")
print(f'Using {device} for inference')
resnet50 = torch.hub.load('NVIDIA/DeepLearningExamples:torchhub', 'nvidia_resnet50', pretrained=True)
utils = torch.hub.load('NVIDIA/DeepLearningExamples:torchhub', 'nvidia_convnets_processing_utils')
resnet50.eval().to(device)

uris = [
     'http://images.cocodataset.org/test-stuff2017/000000024309.jpg',
     'http://images.cocodataset.org/test-stuff2017/000000028117.jpg',
     'http://images.cocodataset.org/test-stuff2017/000000006149.jpg',
     'https://product.hstatic.net/1000372317/product/z2333595235353_5c125d6a81cdce01a7f31e4825c44e89_a4619c971e5a402aa1d3229e409b2326_master.jpg',
     'http://images.cocodataset.org/test-stuff2017/000000004954.jpg',
]
batch = torch.cat(
    [utils.prepare_input_from_uri(uri) for uri in uris]
).to(device)

PATH = 'C:/Users/thanhduong05/cifar_resnet50.pth'
#trình tối ưu hóa
optimizer = optim.SGD(resnet50.parameters( ), lr=0.001, momentum=0.9)

#with torch.storage.map_location('cpu'):
    #torch.load(open('offending_file.pkl', 'rb'))

#tải mô hình
model = torch.load(PATH)
model.module.state_dict()
torch.nn.DataParallel
model.eval()
