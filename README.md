# memo


"Failed to load platform plugin "xcb" 

sudo ./conda remove qt
sudo ./conda remove pyqt
sudo ./conda install qt
sudo ./conda install pyqt


matplot can't acces qt backend
http://stackoverflow.com/questions/4930524/how-can-i-set-the-backend-in-matplotlib-in-python

import matplotlib
matplotlib.use('Agg')

---------------
INPUT=input
OUTPUT=final_result

#TYPE=QUANTIZED_UINT8
TYPE=FLOAT

MODEL=smile-mobilenet_0.25_128
INFILE=tf_files/${MODEL}-retrained_graph.pb
OUTFILE=tf_files/${MODEL}-optimized_graph.${TYPE}.lite

IMAGE_SIZE=128
MEAN=128 
STD=128
MIN=0
MAX=6
  #--mean_values=128 \
  #--std_values=127

#  --output_array=MobilenetV1/Predictions/Reshape_1 \
  
toco \
  --input_file=$INFILE \
  --output_file=$OUTFILE \
  --input_format=TENSORFLOW_GRAPHDEF \
  --output_format=TFLITE \
  --inference_type=$TYPE \
  --input_data_type=FLOAT \
  --input_shape=1,${IMAGE_SIZE},${IMAGE_SIZE},3 \
  --input_array=$INPUT \
  --output_array=$OUTPUT \
  --mean_value=$MEAN \
  --std_value=$STD \
  --default_ranges_min=$MIN \
  --default_ranges_max=$MAX 
    
  #--input_shapes=1,${IMAGE_SIZE},${IMAGE_SIZE},3 \
  #--input_arrays=input \
  #--output_arrays=final_result \

