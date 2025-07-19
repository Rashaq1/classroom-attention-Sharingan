# classroom-attention-Sharingan
using Sharingan method for classroom attention detection 
# 🎯 Classroom Attention Detection using Sharingan

This project is based on the [Sharingan](https://github.com/idiap/sharingan) model from CVPR 2024, originally developed for multi-person gaze prediction in crowds. We adapt and extend it for classroom settings to analyze **student attention behavior** using gaze direction.

## 📌 What It Does

- 🧠 Detects student heads using YOLOv5 pretrained on the **CrowdHuman** dataset
- 🔁 Tracks each student across frames using `OcSort` tracker
- 👁️ Predicts gaze direction using the **Sharingan** transformer model
- 🔍 Visualizes gaze as vectors, heatmaps, and attention scores
- 📦 Outputs an annotated video with real-time gaze visualization

## 🛠️ How It Works

1. **YOLOv5 + CrowdHuman**  
   Used to detect **heads only** (not full body or other objects) for better classroom relevance.

2. **OcSort Tracker**  
   Assigns a **unique ID per student** across frames so we can track individuals and build attention maps over time.

3. **Sharingan Model**  
   A custom transformer model trained to output:
   - Gaze vector 🡺 direction of attention
   - Gaze point 🡺 where the person is looking in the frame
   - Heatmap 🡺 visual area of attention
   - In/Out score 🡺 whether the person is looking inside the scene or outside

4. **Visualization**  
   The system uses OpenCV to draw arrows, circles, and heatmaps directly on the output video.

## 🚀 Quickstart

### 1. Clone the Repo

```bash
git clone https://github.com/Rashaq1/classroom-attention-Sharingan.git
cd classroom-attention-Sharingan
2. Setup Environment
conda create -n sharingan python=3.9
conda activate sharingan
pip install -r requirements.txt
3. Download Model Weights
Due to size limitations, you must manually download model weights from Google Drive:

📥 Download Weights : https://drive.google.com/drive/folders/1xfGfdKdsG8Oa7T-VZPdf6-FMNrcLo2rQ?usp=share_link

File Name	Destination Folder
videoattentiontarget.pt	checkpoints/
yolov5m_crowdhuman.pt	weights/
gazefollow.pt (optional)	checkpoints/
childplay.pt (optional)	checkpoints/
4. Run the Demo
python demo.py --input-dir data --input-filename Classroom_Video.MP4 --output-dir data --show-gaze-vec
Make sure your video is placed under the data/ directory and the models are in the correct paths.
📈 Output Example

The output video will show:

🔵 Gaze direction arrows
🔥 Heatmap overlay for selected student
🆔 Consistent ID tracking for each student
⚠️ Notes

This implementation is computationally heavy — a 4-minute video can take hours to process on CPU.
Real-time performance is not guaranteed out-of-the-box but can be optimized.
📚 Citation

If you use this work or the Sharingan model, please cite:

Tafasca, S., Ba, S., & Odobez, J.-M. (2024). Sharingan: A Transformer Architecture for Multi-Person Gaze Following. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR).
Read the paper : https://openaccess.thecvf.com/content/CVPR2024/papers/Tafasca_Sharingan_A_Transformer_Architecture_for_Multi-Person_Gaze_Following_CVPR_2024_paper.pdf

🤝 Contributions

Customized, tested, and adapted by @Rashaq1
Original model by @idiap/sharingan
