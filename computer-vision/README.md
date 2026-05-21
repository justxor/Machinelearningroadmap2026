# 👁️ Computer Vision Engineering — a practical course

The sixth modular course of this repository. From basic image operations to production systems for detection, segmentation, OCR, tracking, and multimodal models. No filler, no academic proofs — only what a CV engineer actually needs in 2026.

## 🎯 Who this course is for

- You know Python and basic DL (PyTorch, training neural networks).
- You want to specialize in CV or strengthen the CV side of a project.
- You need applied skills: not "trained a CNN on MNIST", but "deployed a detector to production with p95 < 50ms".

**If you do not have the basics:** start with [math-for-ml](../math-for-ml/README.md) and [neural-networks](../neural-networks/README.md). This course assumes you understand what a convolution and a training loop are.

## 📚 Course structure

**21 lessons, 4 blocks + 3 capstones.**

### Block 1. CV foundations

- [01. Digital images and basic operations](./01-image-basics.md) — pixels, formats, color spaces, OpenCV.
- [02. Classical CV algorithms](./02-classical-cv.md) — filters, edges, features (SIFT, ORB), homography.
- [03. Augmentations and data pipelines](./03-augmentations.md) — albumentations, batch processing, custom transforms.
- [04. CV metrics](./04-metrics.md) — accuracy, IoU, mAP, panoptic quality.
- [05. Backbones and transfer learning](./05-backbones.md) — ResNet, EfficientNet, ConvNeXt, fine-tuning strategies.

### Block 2. Core tasks

- [06. Image classification](./06-classification.md) — from baseline to SOTA, multi-label, imbalance.
- [07. Object detection](./07-detection.md) — YOLO, DETR, RT-DETR, anchor-based vs anchor-free.
- [08. Semantic segmentation](./08-semantic-segmentation.md) — U-Net, DeepLab, Mask2Former.
- [09. Instance and panoptic segmentation](./09-instance-segmentation.md) — Mask R-CNN, SAM 2.
- [10. Keypoint detection and pose estimation](./10-keypoints-pose.md) — HRNet, MediaPipe.
- [11. Object tracking](./11-tracking.md) — SORT, ByteTrack, multi-object tracking.

### Block 3. Vision Transformers and multimodality

- [12. Vision Transformers](./12-vision-transformers.md) — ViT, Swin, DINO, MAE.
- [13. CLIP and multimodal models](./13-clip-multimodal.md) — zero-shot classification, image-text retrieval.
- [14. VLM: vision-language models](./14-vlm.md) — LLaVA, Qwen-VL, Florence-2, OCR tasks.
- [15. Generative models for CV](./15-generative-cv.md) — Stable Diffusion, ControlNet, inpainting, super-resolution.

### Block 4. Production

- [16. OCR and document recognition](./16-ocr.md) — Tesseract, PaddleOCR, donut, LayoutLM.
- [17. Video analytics](./17-video-analytics.md) — temporal models, action recognition, real-time pipelines.
- [18. Edge and mobile inference](./18-edge-mobile.md) — ONNX, CoreML, TFLite, NVIDIA Jetson, quantization.
- [19. Deploying CV models to production](./19-production-deploy.md) — Triton, FastAPI, batching, GPU pooling.
- [20. Monitoring and MLOps for CV](./20-monitoring-mlops.md) — drift on images, retraining, A/B tests of visual models.
- [21. Security and privacy in CV](./21-safety-privacy.md) — adversarial attacks, deepfake detection, face anonymization, data licensing.

### 🎯 Capstone projects

- [Capstone 1. End-to-end object detector on your own dataset](./capstone-1-detector.md) — from collection and labeling to deployment.
- [Capstone 2. Real-time video analytics with tracking](./capstone-2-video-analytics.md) — detection + tracking + counting + dashboard.
- [Capstone 3. Multi-modal RAG over images and documents](./capstone-3-multimodal-rag.md) — VLM + OCR + retrieval + LLM.

## 🛠️ Course stack

**Core:** Python 3.12+, PyTorch 2.x, OpenCV, Pillow, albumentations.

**Models:** torchvision, timm (CNN/ViT models), ultralytics (YOLO), Hugging Face transformers.

**Deployment:** ONNX, ONNX Runtime, NVIDIA Triton, FastAPI, Docker.

**Eval:** torchmetrics, COCO API, FiftyOne.

**Annotation:** CVAT, Label Studio, Roboflow.

## ⏱️ How long it takes

- **Intensive (25+ h/week):** 6-8 weeks.
- **Alongside a job (10-12 h/week):** 4-6 months.
- **Relaxed pace (5-7 h/week):** 9-12 months.

**Rule:** one topic per week + one practical artifact. Do not rush — better deep across 21 topics than shallow across 50.

## 🎯 What you will leave with

- **Inside-out understanding:** from pixels to Vision Transformers — no black boxes.
- **6 ready architectures:** classifier, detector, segmenter, tracker, VLM app, OCR pipeline.
- **3 production-ready capstones** for your portfolio.
- **Solid MLOps for CV:** drift detection, A/B tests of visual models, edge deployment.
- **Trade-off awareness:** YOLO vs DETR, full fine-tune vs transfer learning, on-device vs cloud.
- **Niche know-how:** OCR, video analytics, medical CV, autonomous systems — where to grow beyond the base.

## 📊 Career context

**Computer Vision Engineer** is one of the most consistently in-demand ML roles. Less hype than LLMs, but more real industry problems: e-commerce (visual search, photo tagging), retail (in-store video analytics), security (face recognition, fraud), medicine (medical imaging), agritech, autonomous vehicles, AR/VR.

**Levels and salaries (international market, 2026, USD gross / year):**

| Level | International |
|-------|---------------|
| Junior CV | $70–110K |
| Middle CV | $120–180K |
| Senior CV | $180–300K |
| Staff/Principal CV | $300–500K+ |

Numbers vary by region — see [levels.fyi](https://www.levels.fyi/) for up-to-date comp by company and city.

**Hot subdomains 2026:** multimodal models (VLM), real-time video (action recognition, tracking), edge AI, foundation models for CV (DINO, SAM), generative CV (stylization, super-res, inpainting), 3D vision, and NeRF.

## 🔗 Relation to other courses

- **Before this course:** [math-for-ml](../math-for-ml/README.md) — you need linear algebra and an understanding of convolutions.
- **In parallel:** [neural-networks](../neural-networks/README.md) — deeper dive into architectures (ViT, MAE).
- **After:** [llm-engineering](../llm-engineering/README.md) for VLM projects; [data-science](../data-science/README.md) for product-side tasks (A/B on CV features).
- **Boost:** [claude-code](../claude-code/README.md) to speed up CV pipeline development.

## 🚫 What this course does NOT have (on purpose)

- **Doomy CNN theory.** No 50 pages of shift-equivariance proofs. Intuition + working code is enough.
- **Outdated models.** AlexNet and VGG appear historically, but we do not train them. The standard is ResNet/EfficientNet/ConvNeXt + ViT/Swin.
- **Hype without practice.** No "10 cool CLIP tricks" — but "how to ship CLIP for image search in production".
- **Generative as an end in itself.** There are applications (super-res, inpainting), but not "how to make AI art".

## 📚 Extra resources

**Courses:**
- [Stanford CS231n](http://cs231n.stanford.edu/) — the classic.
- [Hugging Face Computer Vision Course](https://huggingface.co/learn/computer-vision-course/) — modern, free.
- [fast.ai Practical Deep Learning](https://course.fast.ai/) — practical-first.

**Books:**
- *Computer Vision: Algorithms and Applications* — Richard Szeliski (free online).
- *Deep Learning for Computer Vision* — Rajalingappaa Shanmugamani.
- *Modern Computer Vision with PyTorch* — V Kishore Ayyadevara.

**Conferences:** CVPR, ICCV, ECCV — the main CV conferences, recap videos on YouTube for free.

**Blogs and Telegram:**
- [Lil'Log](https://lilianweng.github.io/) — deep technical write-ups.
- [Roboflow Blog](https://blog.roboflow.com/) — practical tutorials.
- [@ai_machinelearning_big_data](https://t.me/ai_machinelearning_big_data) — CV model releases.

## ✅ Readiness checklist

- [ ] Python at the "I write scripts and classes freely" level.
- [ ] PyTorch: I understand Dataset, DataLoader, the training loop.
- [ ] I have intuition for CNNs (convolution, pooling).
- [ ] I have a GPU (at least RTX 4060 locally) or am OK with Colab/Kaggle.
- [ ] Basic Git and Docker.

**If any item is unchecked:** go back to the base courses before starting.

---

▶︎ Start: [01-image-basics.md](./01-image-basics.md)
