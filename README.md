env start

conda activate MCS_25   

conda activate NISQA - new one

info

ffprobe amused_1-15_0001.wav

delka?

soxi -T -D *.wav

prekodovani na pcm_s16le

ffmpeg -i amused_1-15_0001.wav -c:a pcm_s16le output-16.wav

bitrate set to 8khz
ffmpeg -i output-16.wav -ar 8000 output-16-8khz.wav


//doesnt work -gsm/libgsm
ffmpeg -i output-16-8khz.wav -c:a libgsm output-16-8khz-gsm.wav

//alternative
ffmpeg -i output-16-8khz.wav -ar 8000 -ac 1 -c:a libopencore_amrnb output-16-8khz-amr.wav

//ar sample rate 8k         b:a  bitrate 12k

ffmpeg -i output-16-8khz.wav -ar 8000 -c:a libopus -b:a 12k output-opus.opus 

ffmpeg -i output-opus.opus -ar 8k output-opus.wav 


ffmpeg -i output-16-8khz.wav -c:a aac -b:a 12k output-aac.aac

//NISQA command folder

python run_predict.py --mode predict_dir --pretrained_model weights/nisqa.tar --data_dir "/Users/zdeni/Mendelu/Navazujici 3/Mobile communication technology/Mobile communication" --num_workers 0 --bs 10 --output_dir "/Users/zdeni/Mendelu/Navazujici 3/Mobile communication technology/Mobile communication/NISQA results"


//NISQA single file

python run_predict.py --mode predict_file --pretrained_model weights/nisqa.tar --deg "/Users/zdeni/Mendelu/Navazujici 3/Mobile communication technology/Mobile communication/output-16-8khz.wav" --output_dir "/Users/zdeni/Mendelu/Navazujici 3/Mobile communication technology/Mobile communication/NISQA results"