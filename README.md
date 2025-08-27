# AI Model


| Model            | Bedrock Availability | Accuracy   | Strengths                          | Weaknesses                                  | Improvement Strategy                                                                 |
|------------------|----------------------|------------|------------------------------------|---------------------------------------------|--------------------------------------------------------------------------------------|
| **LLaVA**        | No (Google Colab)    | ~30%       | Detailed outputs, contextual       | Very low disease accuracy                    | Fine-tune on a strawberry disease dataset (white/grey/black mould) using LoRA; add pre-processing filters for color correction |
| **Amazon Nova**  | Yes                  | ~30–35%    | Contextual reasoning attempts      | Poor fruit & disease detection               | Train with fruit detection bounding boxes; integrate pre-trained object detection (YOLOv8/Faster R-CNN) before passing crops to Nova |
| **Claude 3**     | Yes                  | —          | Consistent context detection       | Confusion between bruise vs. disease         | Provide prompt engineering with step-by-step reasoning + fine-tune with labeled disease vs bruise datasets |
| **Pixtral (Mistral)** | Yes             | ~50–60%    | Best anomaly detection, mould awareness | Confused between similar colors of fungi | Add color-normalization pre-processing (remove lighting variance); fine-tune on labelled strawberry disease images |
