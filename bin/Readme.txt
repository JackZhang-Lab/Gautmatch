GPU 1,2,3 ...

(1) check your GPUs 
cat /proc/driver/nvidia/gpus/*/information
nvidia-smi

(2) know about the  SM (streaming multiprocessor):
https://en.wikipedia.org/wiki/CUDA#GPUs_supported
The Compute capability (version) in the table relects the same number as SM

(3) check your cuda library:
ls /usr/local/
which nvcc
locate libcudart.so


###############################################
################ ribosome test ################

### quick view of the autopicked results, run this command:
./Gautomatch_display test8.mrc 1.33 200

#get your own results using any of the following command:
### (1) automatically generated Guassian templates
Gautomatch--apixM 1.34  --diameter 240 --max_dist 200 --cc_cutoff 0.25 --lave_D 300 -lsigma_cutoff 1.3 --lsigma_D 200 --speed 2 --extract_raw test7.mrc test8.mrc

### (2) using white templates to pick black micrograph
Gautomatch  --apixM 1.34 --apixT 5.36 --T templates_white.mrcs --diameter 240 --max_dist 200 --cc_cutoff 0.45 test7.mrc test8.mrc

### (3) using black templates to pick black micrograph, MUST specify --dont_invertT in this case
Gautomatch --apixM 1.34 --apixT 5.36 --T templates_black.mrcs --dont_invertT --diameter 240 --min_dist 200 --cc_cutoff 0.45 --lave_D 300 -lsigma_cutoff 1.3 --lsigma_D 200 --speed 2 --extract_raw test7.mrc test8.mrc

### (4) the same as (3) but using lightly lower speed,  --speed 1
Gautomatch --apixM 1.34  --apixT 5.36 --T templates_black.mrcs --dont_invertT --diameter 240 --min_dist 200 --cc_cutoff 0.45 --lave_D 300 -lsigma_cutoff 1.3 --lsigma_D 200 --speed 1 --extract_raw test7.mrc test8.mrc 

### (5) the same as (3) but output diagnotic files
Gautomatch test7.mrc test8.mrc --apixM 1.34  --apixT 5.36 --T templates_black.mrcs --dont_invertT --diameter 240 --min_dist 200 --cc_cutoff 0.45 --lave_D 300 -lsigma_cutoff 1.3 --lsigma_D 200  --extract_raw --write_ccmax_mic --write_bg_mic --write_bgfree_mic --write_lsigma_mic --write_mic_mask


