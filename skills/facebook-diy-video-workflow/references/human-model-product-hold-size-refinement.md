# Human-Model Product-Holding Size and Refinement Pass

Use this operational supplement after selecting exactly one original human-model first-frame prompt. Apply it when product scale matters, the person must hold the product naturally toward the camera, the user requests multiple versions, or a product-center mosaic reference is needed for refinement.

Keep this file separate from the selected source prompt. Do not edit, merge, or replace either original prompt in `human-model-prompts/`.

## Required Inputs

- A clean real-product reference that establishes product identity, structure, colors, border, and aspect ratio.
- Exact dimensions, a size-comparison image, or one user-approved scale frame. A generated image is not dimension evidence unless the user explicitly approves it as the scale anchor.
- The character and outfit description.
- The exact person-product action.
- The requested number of independent 9:16 versions.
- Scene, camera, lighting, and negative constraints.

If the available evidence cannot establish product scale, stop this branch and request only the missing size evidence. Do not estimate dimensions from the product category.

## Pass 1: Lock Scale and Natural Contact

1. Create a scale lock before generation: product aspect ratio, orientation, size relative to the torso and hands, intended frame occupancy, visible borders, and the hand contact points.
2. Treat the real product reference as the product-identity source and the dimensions or approved scale frame as the scale source. Do not let a text description override either image.
3. Keep the load-bearing relationship physically believable. Prefer one relaxed hand supporting the lower edge while the other stabilizes a side edge, or two hands supporting the lower side corners. Avoid fingertip-only pinching, perfectly mirrored elbows, hidden thumbs, wrists bent beyond a comfortable angle, or fingers painted onto the product surface.
4. Keep the product close enough to share toward the lens without hiding the person's eyes or mouth. Preserve a small gap between the upper product edge and the chin when the composition allows it.
5. Generate the scale-calibration frame before asking for texture or beauty refinements. When the user requests two versions, create two separate 9:16 files, never a collage, grid, split screen, or combined image.

## Full-Size Gate

Inspect every version at full size. Reject a frame when any of the following is wrong:

- The product aspect ratio, apparent size, border, orientation, or perspective differs from the scale source.
- A hand floats, intersects the product, loses a finger, duplicates a finger, or fails to carry the product's weight.
- The grip would be painful or impossible to hold for several seconds.
- The product blocks the eyes or mouth, the face identity drifts, or skin texture changes between the face and hands.
- The product structure, pattern, material, label, or color departs from the real-product reference.

Approve scale and contact before continuing. A refinement pass must not be used to hide a structurally wrong frame.

## Pass 2: Same-Canvas Product-Center Mosaic Refinement

After a scale-calibration frame passes:

1. Keep the approved unmodified frame as the composition, person, hand-contact, and scale anchor.
2. Duplicate it as a separate reference with exactly the same pixel dimensions, aspect ratio, crop, and canvas. Do not resize, pad, crop, stretch, or overwrite the approved frame.
3. Apply fog mosaic or coarse pixelation only to the interior center of the product. Keep the complete outer border, all four corners, silhouette, perspective edges, both hands, every contact point, face, clothing, and background visible and unchanged.
4. Upload three clearly labeled inputs for the refinement pass:
   - Real product reference: product identity, structure, pattern, material, and color source.
   - Approved scale frame: person identity, pose, composition, product dimensions, and grip source.
   - Same-canvas mosaic reference: the product-center region to restore or refine while all visible anchors stay frozen.
5. Instruct the image model to refine only the mosaicked product-center region from the real product reference. Freeze the approved product border, apparent size, perspective, location, hands, contact points, person, camera, lighting, background, and 9:16 canvas.
6. Save the refined result as a new file and retain the approved scale frame plus the mosaic reference for comparison.

The product-center mosaic is an image-refinement aid, not face masking. Do not route it through the face-mask module or apply it to the person.

## Two-Version Runtime Example

Supply these facts separately beside the unchanged natural-lifestyle source prompt:

```text
输出：生成 A、B 两个版本，共两张彼此独立的 9:16 图片。禁止拼图、宫格、分屏或合并出图。

人物与穿搭：43 岁美国白人中年女性，脸型柔和饱满，气质温婉从容。浅棕褐中长发带自然微卷，半随意挽在耳后，碎发自然散落，发型蓬松不刻意。日常伪素颜淡妆，轻薄底妆保留自然皮肤纹理，浅棕自然眉形，无浓重眼妆，只涂淡奶茶色润唇膏。黑色连衣裙外搭深燕麦色宽松软糯针织开衫，指甲修剪整齐并涂裸色透明甲油，手腕戴细款素圈金手链。

两版共同动作：产品的画面尺寸、长宽比和相对人物大小严格匹配图一。人物双手拿稳产品，准备把产品轻轻靠近镜头，像在自然分享刚发现的好物。肩膀、手肘、手腕、手指和拇指保持放松并真实承重。产品位于画面中间且完整可见，不遮挡人物眼睛和嘴。产品外框、结构、颜色和透视严格依据参考图。

A 版：一只手自然托住产品下边缘，另一只手稳定侧边；产品基本正对镜头，仅有轻微自然后倾。

B 版：双手分别托住产品两个下侧角，左右手肘高度略有差异；产品比 A 版更靠近镜头，但尺寸仍严格锁定图一。

场景与拍摄：真实美国家居环境，iPhone 15 Pro 原生相机手持拍摄，平视微俯视角，轻微自然手持感。暖调自然光，背景自然虚化，焦点落在产品和双手接触关系上；保留真实皮肤纹理和产品表面自然反光，整体像随手记录的 UGC 生活画面。

负面约束：无棚拍感，无打光板痕迹，无夸张浓妆，无网红摆拍姿势，无过度磨皮美颜，无字幕水印，无夸张滤镜，无僵硬假笑，无杂乱违和背景；禁止产品变形、尺寸漂移、拇指消失、手指悬空、多余手指、手掌融合或产品挡住眼睛和嘴。
```

## Delivery Checklist

- Every requested version is a separate 9:16 file.
- The product scale matches the approved scale source.
- The grip and load-bearing contact are physically believable.
- The original product reference, approved scale frame, and same-canvas mosaic reference are all supplied to the refinement pass.
- The mosaic covers only the product center and leaves scale and contact anchors visible.
- The refined result changes only the product-center region.
- The unmodified approved frame and processed reference remain separate files.
