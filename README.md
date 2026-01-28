# 
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>品牌中心素材库 - 工单版</title>
    <style>
        :root {
            --primary-blue: #e6f4ff;
            --primary-text: #000000;
            --active-text: #1890ff;
            --border-color: #f0f0f0;
            --bg-gray: #f5f7fa;
        }

        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; height: 100vh; display: flex; color: #333; overflow: hidden; }

        /* --- 左侧侧边栏 --- */
        aside {
            width: 240px;
            background: #fff;
            border-right: 1px solid #e8e8e8;
            display: flex;
            flex-direction: column;
            flex-shrink: 0;
        }

        .logo-area {
            padding: 20px;
            font-size: 18px;
            font-weight: 600;
            border-bottom: 1px solid #f0f0f0;
        }

        .filter-bar {
            padding: 10px;
            display: flex;
            gap: 5px;
            border-bottom: 1px solid var(--border-color);
            background: #fff;
        }

        .filter-btn {
            flex: 1;
            padding: 6px 0;
            text-align: center;
            background: #f5f5f5;
            border: 1px solid transparent;
            font-size: 12px;
            color: #666;
            cursor: pointer;
            border-radius: 4px;
            transition: all 0.2s;
        }
        .filter-btn:hover { background: #e6f7ff; color: #1890ff; border-color: #bae7ff; }
        .filter-btn.active {
            background: #1890ff;
            color: #fff;
            box-shadow: 0 2px 4px rgba(24,144,255,0.2);
            font-weight: 500;
            border-color: #1890ff;
        }

        .sidebar-list {
            flex: 1;
            overflow-y: auto;
            padding: 10px 0;
        }

        .sidebar-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 20px;
            cursor: pointer;
            font-size: 13px;
            transition: all 0.2s;
            margin-bottom: 2px;
            border-left: 3px solid transparent;
        }

        .sidebar-item:hover { background-color: #fafafa; }
        
        .sidebar-item.active {
            background-color: var(--primary-blue);
            color: var(--active-text);
            border-left: 3px solid var(--active-text);
        }

        .count-tag {
            background: #f0f0f0;
            color: #999;
            padding: 1px 8px;
            border-radius: 10px;
            font-size: 11px;
        }
        .sidebar-item.active .count-tag {
            background: #fff;
            color: var(--active-text);
        }

        /* --- 右侧内容区 --- */
        main {
            flex: 1;
            background: #f7f8fa;
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }

        .top-header {
            padding: 15px 30px;
            background: #fff;
            border-bottom: 1px solid #e8e8e8;
            flex-shrink: 0;
        }

        .page-title { font-size: 18px; font-weight: 600; margin-bottom: 5px; color: #333; }
        .page-desc { font-size: 12px; color: #999; }

        .content-area {
            flex: 1;
            overflow-y: auto;
            padding: 20px 30px;
        }

        /* 分组区块 */
        .group-block { 
            background: #fff;
            margin-bottom: 25px; 
            border: 1px solid #e8e8e8; 
            border-radius: 8px; 
            box-shadow: 0 1px 3px rgba(0,0,0,0.02);
            overflow: hidden;
        }
        
        .group-header {
            background: #fff;
            padding: 15px 20px;
            font-weight: 600;
            font-size: 15px;
            border-bottom: 1px solid #f0f0f0;
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .group-total {
            font-size: 12px;
            color: #666;
            background: #f5f5f5;
            padding: 2px 8px;
            border-radius: 4px;
        }

        /* 子分组区块 */
        .sub-group-block {
            padding: 20px;
        }

        .sub-group-title {
            font-size: 14px;
            color: #333;
            margin-bottom: 15px;
            border-left: 4px solid #1890ff;
            padding-left: 10px;
            font-weight: 600;
            line-height: 1.2;
        }

        /* 图片网格 */
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
            gap: 20px;
        }

        .card {
            background: #fff;
            border: 1px solid #eee;
            border-radius: 6px;
            overflow: hidden;
            transition: all 0.2s;
            cursor: pointer;
        }
        .card:hover { 
            box-shadow: 0 8px 16px rgba(0,0,0,0.08); 
            transform: translateY(-2px);
            border-color: #d9d9d9;
        }

        .card-img-wrapper {
            width: 100%;
            height: 180px;
            background: #f0f2f5;
            position: relative;
            overflow: hidden;
        }

        .card-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
            transition: transform 0.3s;
        }
        .card:hover .card-img { transform: scale(1.03); }

        .card-body { padding: 12px; }
        
        .tag-row { margin-bottom: 10px; }
        .type-tag {
            background: #e6f7ff;
            color: #1890ff;
            font-size: 12px;
            padding: 2px 8px;
            border-radius: 4px;
            border: 1px solid #bae7ff;
            display: inline-block;
        }

        .info-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 12px;
            color: #888;
            margin-bottom: 4px;
            line-height: 1.4;
        }
        
        .info-val { color: #555; font-weight: 500; }

        /* 弹窗 */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0; top: 0;
            width: 100%; height: 100%;
            background-color: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(3px);
        }
        .modal-content {
            background-color: #fff;
            width: 90%;
            max-width: 1000px;
            height: 85vh;
            display: flex;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 12px 48px rgba(0,0,0,0.15);
        }
        .m-img-box {
            flex: 1.5;
            background: #ffffff; /* 按照要求改为白色背景 */
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
            border-right: 1px solid #f0f0f0;
        }
        .m-img-box img { max-width: 100%; max-height: 100%; object-fit: contain; box-shadow: 0 4px 12px rgba(0,0,0,0.1); }
        
        .m-info-box {
            flex: 1;
            padding: 30px;
            overflow-y: auto;
            position: relative;
            display: flex;
            flex-direction: column;
            gap: 20px;
            background: #fff;
        }
        .close {
            position: absolute;
            right: 20px; top: 15px;
            font-size: 28px;
            cursor: pointer;
            color: #ccc;
            line-height: 1;
            transition: color 0.2s;
        }
        .close:hover { color: #333; }
        
        .m-section { margin-bottom: 10px; }
        .m-title { 
            font-size: 15px; 
            font-weight: 700; 
            margin-bottom: 12px; 
            padding-bottom: 8px; 
            border-bottom: 1px solid #eee; 
            color: #333;
        }
        
        .m-row { display: flex; font-size: 13px; line-height: 1.6; margin-bottom: 6px; }
        .m-label { color: #999; width: 80px; flex-shrink: 0; }
        .m-val { color: #333; word-break: break-all; }
        
        .m-prompt {
            background: #f7f8fa;
            padding: 15px;
            border-radius: 6px;
            font-size: 13px;
            color: #444;
            white-space: pre-wrap;
            border: 1px solid #eee;
            margin-top: 5px;
            line-height: 1.6;
        }
    </style>
</head>
<body>

<aside>
    <div class="logo-area">品牌中心</div>
    <div class="filter-bar">
        <button class="filter-btn active" onclick="switchMode('SPU', this)">按SPU</button>
        <button class="filter-btn" onclick="switchMode('TIME', this)">按时间</button>
        <button class="filter-btn" onclick="switchMode('ORDER', this)">按工单</button>
    </div>
    <div class="sidebar-list" id="sidebarList">
        <!-- JS填充 -->
    </div>
</aside>

<main>
    <div class="top-header">
        <div class="page-title" id="pageTitle">全部图片</div>
        <div class="page-desc" id="pageCount">共 0 张图</div>
    </div>
    <div class="content-area" id="content">
        <!-- JS填充 -->
    </div>
</main>

<!-- 详情弹窗 -->
<div id="myModal" class="modal">
    <div class="modal-content">
        <div class="m-img-box"><img id="mImg" src=""></div>
        <div class="m-info-box">
            <span class="close" onclick="closeModal()">&times;</span>
            
            <div class="m-section">
                <div class="m-title">基础信息</div>
                <div class="m-row"><span class="m-label">ID:</span><span class="m-val" id="mID"></span></div>
                <div class="m-row"><span class="m-label">SPU:</span><span class="m-val" id="mSPU"></span></div>
                <div class="m-row"><span class="m-label">SKU:</span><span class="m-val" id="mSKU"></span></div>
                <div class="m-row"><span class="m-label">工单号:</span><span class="m-val" id="mOrder"></span></div>
            </div>

            <div class="m-section">
                <div class="m-title">生产详情</div>
                <div class="m-row"><span class="m-label">分类:</span><span class="m-val" id="mType"></span></div>
                <div class="m-row"><span class="m-label">BU:</span><span class="m-val" id="mBU"></span></div>
                <div class="m-row"><span class="m-label">BG:</span><span class="m-val" id="mBG"></span></div>
                <div class="m-row"><span class="m-label">操作人:</span><span class="m-val" id="mUser"></span></div>
                <div class="m-row"><span class="m-label">时间:</span><span class="m-val" id="mTime"></span></div>
                <div class="m-row"><span class="m-label">模型:</span><span class="m-val" id="mModel"></span></div>
            </div>

            <div class="m-section">
                <div class="m-title">资源链接</div>
                <div class="m-row"><span class="m-label">URL:</span><span class="m-val"><a id="mURL" href="#" target="_blank" style="color:#1890ff;text-decoration:none;">点击打开原图</a></span></div>
            </div>

            <div class="m-section" style="flex:1; display:flex; flex-direction:column; min-height: 0;">
                <div class="m-title">提示词 (Prompt)</div>
                <div style="flex:1; overflow-y:auto; border:1px solid #eee; border-radius:6px;">
                    <div class="m-prompt" id="mPrompt" style="margin:0; border:none; min-height:100%;"></div>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
// 完整CSV数据 (包含第12列工单号)
const rawData = `id,SPU,sku,生成时间,URL,BU,BG,操作人,提示词,模型,提示词分类,工单号
1,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx551767765969939039.jpeg,品牌BU,品牌BG,陈笑,"场景图提示词...",gemini-3-pro-image-preview,场景图,D202601060056
2,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx351767765942680515.jpeg,品牌BU,品牌BG,陈笑,"白底图提示词...",gemini-3-pro-image-preview,白底主图,D202601070110
3,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx411767766060795343.jpeg,品牌BU,品牌BG,陈笑,"细节图提示词...",gemini-3-pro-image-preview,细节图,D202601070110
4,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx491767766089185756.jpeg,品牌BU,品牌BG,陈笑,"细节图提示词...",gemini-3-pro-image-preview,细节图,D202601070110
5,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767766119695254.jpeg,品牌BU,品牌BG,陈笑,"细节图提示词...",gemini-3-pro-image-preview,细节图,D202601070110
6,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951767766014929811.jpeg,品牌BU,品牌BG,陈笑,"场景图提示词...",gemini-3-pro-image-preview,场景图,D202601070110
7,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx391767766209395703.jpeg,品牌BU,品牌BG,陈笑,"尺寸图提示词...",gemini-3-pro-image-preview,尺寸图,D202601070110
8,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx641767772050865006.jpeg,品牌BU,品牌BG,陈笑,"场景...",gemini-2.5-flash-image,场景,D202601070110
9,PHO_116I,PHO_116ISIAE,2026-01-07T06:11:48,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx651767766168481549.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070110
10,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx341767771619654231.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070123
11,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx831767771492559154.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070123
12,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941767770687280788.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070123
13,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx401767771817656693.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-2.5-flash-image,场景,D202601070123
14,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx901767771673211769.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070123
15,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951767771585219889.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070123
16,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx371767771704456420.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070123
17,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx231767770836616610.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070123
18,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx801767770720718925.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070181
19,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx651767771644988782.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070181
20,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx411767770788845067.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070181
21,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx791767771048581460.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-2.5-flash-image,场景,D202601070181
22,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx341767770896554427.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070181
23,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx861767770927889097.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070181
24,PHK_33U7,PHK_33U7MGPE,2026-01-07T07:49:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx891767770864158639.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070181
25,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx581767775308046885.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070181
26,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx581767774288988888.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
27,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx311767774808330512.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-2.5-flash-image,场景,D202601070204
28,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx971767774253580451.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
29,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741767774462264287.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
30,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx891767774410901773.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
31,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx611767774192150773.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070204
32,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181767775274811605.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070204
33,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx481767774321602123.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
34,PPS_3346,PPS_3346GP83,2026-01-07T08:34:03,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx521767774374252141.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
35,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx441767775338151782.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
36,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx641767775849971156.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601070204
37,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx911767775565857611.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
38,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx781767775522562164.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
39,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771767775608945599.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,D202601070204
40,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141767776229920103.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070204
41,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx551767775471830285.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
42,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571767776440515164.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
43,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx381767776444205401.jpeg,品牌BU,品牌BG,陈笑,"尺寸...",gemini-2.5-flash-image,场景,D202601070204
44,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx721767776266546182.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
45,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx421767776326905866.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
46,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx991767776300315507.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
47,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141767776473096288.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
48,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx271767776899357172.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
49,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx601767777089406065.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
50,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx621767776560468393.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,D202601070204
51,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141767776979574540.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
52,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561767776866557176.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
53,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx441767777235516449.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,D202601070204
54,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx161767777036958581.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
55,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx721767776832964540.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070204
56,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx751767777631462775.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070204
57,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx361767777153686923.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070204
58,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx671767777854510449.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,D202601070256
59,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851767777587034328.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070256
60,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx511767777740117825.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
61,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx191767777827874109.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
62,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181767777794267839.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
63,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx481767777675396056.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070256
64,PHK_3456,PHK_3456MCPP,2026-01-07T09:29:20,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx541767777761568135.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
65,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941767778484757419.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
66,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741767778520176535.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
67,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx471767778400870159.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070256
68,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx761767778466626482.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070256
69,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx821767778368699977.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070256
70,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx221767778544478418.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
71,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx761767778603875012.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
72,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx391767779149257105.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070256
73,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx201767779363124053.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601070256
74,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561767779038166643.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601070256
75,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx401767779095665988.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070256
76,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx251767779258244088.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
77,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx641767779306227864.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
78,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx971767779455158473.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601070256
79,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx811767779928709909.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601070256
80,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx381767778665246365.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,D202601070256
81,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx801767779358452868.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601070256
82,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx961767780078934261.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080163
83,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx111767779881649315.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601080163
84,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741767779972651321.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601080163
85,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291767780045385453.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080163
86,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx791767780166200051.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080163
87,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx781767780139607901.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080163
88,PHK_35UL,PHK_35ULFG9A,2026-01-07T10:05:39,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx451767780274754316.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601080163
89,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx321767865856083796.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601080163
90,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx801767865888197210.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601080203
91,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx521767865946929337.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080203
92,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx791767865977213713.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080203
93,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx171767865916049240.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601080203
94,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx341767866008271040.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080203
95,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx151767868170121459.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601080203
96,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx991767926804787346.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-3-pro-image-preview,场景,D202601080203
97,PHK_369D,PHK_369DSUT8,2026-01-13T06:12:24,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx151767866036718285.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601080203
98,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx321767927018749072.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-3-pro-image-preview,场景,D202601090231
99,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741767924605382599.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
100,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx611767925555128619.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-3-pro-image-preview,场景,D202601090231
101,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx641767924754551088.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
102,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741767924733545000.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-3-pro-image-preview,场景,D202601090231
103,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771767924637511059.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-3-pro-image-preview,场景,D202601090231
104,PBE_0BZ7,PBE_0BZ7GV85,2026-01-16T12:11:16,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881767924546830785.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601090231
105,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx971767949335002117.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
106,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx371767949296766130.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601090231
107,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561767949364463451.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
108,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571767949995216502.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601090231
109,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571767949995216502.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601090231
110,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571767949995216502.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601090231
111,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx621767949398138834.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
112,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx231767949424478690.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
113,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950041072064.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
114,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571767949995216502.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601090231
115,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950041072064.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
116,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950041072064.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
117,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950041072064.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
118,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981767950117650398.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
119,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981767950117650398.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
120,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981767950117650398.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
121,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981767950117650398.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
122,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881767950159453467.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
123,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881767950159453467.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
124,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881767950159453467.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
125,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881767950159453467.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
126,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950916773810.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
127,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx371767950206488735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
128,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx371767950206488735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
129,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx371767950206488735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
130,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950916773810.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
131,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950916773810.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
132,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101767950916773810.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
133,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx371767950206488735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
134,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx811767950266134495.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
135,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx811767950266134495.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
136,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx811767950266134495.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
137,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx811767950266134495.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
138,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851767950669440746.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
139,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851767950669440746.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
140,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851767950669440746.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
141,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx271767950325399273.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
142,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx271767950325399273.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
143,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx271767950325399273.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
144,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx271767950325399273.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,D202601090231
145,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851767950669440746.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601090231
146,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141768540176860141.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
147,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141768540176860141.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
148,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx501768540199550369.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
149,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx501768540199550369.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
150,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx501768540199550369.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
151,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx501768540199550369.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
152,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141768540176860141.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
153,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141768540176860141.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
154,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx161768540226793739.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
155,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx161768540226793739.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601090231
156,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx161768540226793739.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
157,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx161768540226793739.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
158,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx281768440724836080.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
159,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx911768442653592571.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,D202601140005
160,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx811768440608699967.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601140005
161,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx531768440665203511.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
162,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561768470923412273.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601140005
163,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561768470923412273.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601140005
164,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561768470923412273.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601140005
165,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561768470923412273.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601140005
166,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx171768470980307833.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
167,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx171768470980307833.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
168,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx171768470980307833.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
169,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx241768440896423628.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
170,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx171768470980307833.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
171,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx581768440843349347.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
172,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768471011543502.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
173,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768471011543502.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
174,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768471011543502.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
175,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768471011543502.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
176,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx131768471071590067.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
177,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx131768471071590067.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
178,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx131768471071590067.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
179,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951768471100583348.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
180,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx131768471071590067.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
181,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951768471100583348.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
182,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951768471100583348.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
183,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951768471100583348.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
184,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741768471132054503.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601140005
185,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741768471132054503.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
186,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741768471132054503.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
187,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741768471132054503.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
188,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx431768472175796735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
189,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx431768472175796735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
190,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx431768472175796735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
191,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx431768472175796735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
192,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941768473538654094.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150309
193,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx391768474070273443.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150350
194,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx391768474070273443.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150350
195,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx391768474070273443.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150350
196,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx391768474070273443.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150350
197,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx241768472935296558.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150500
198,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx991768472537596266.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601150500
199,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851768474096441904.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150500
200,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851768474096441904.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150500
201,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851768474096441904.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150500
202,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx861768473497950307.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150500
203,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101768472765979406.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150500
204,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx851768474096441904.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601150500
205,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx381768472982376770.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
206,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881768472958831231.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
207,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771768474130399236.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
208,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771768474130399236.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
209,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771768474130399236.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
210,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771768474130399236.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
211,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx611768474371134400.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
212,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx611768474371134400.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160236
213,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx611768474371134400.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
214,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx581768474157743020.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
215,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx581768474157743020.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
216,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx581768474157743020.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
217,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx581768474157743020.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
218,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx611768474371134400.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
219,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx631768474397573735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
220,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx631768474397573735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
221,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx631768474397573735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
222,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768475163060335.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
223,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981768474877860908.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
224,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx631768474397573735.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
225,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx541768474815910355.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
226,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981768474925790568.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
227,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx551768474785048889.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601160242
228,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941768475689869242.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
229,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476041229404.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
230,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476041229404.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
231,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941768475689869242.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
232,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476041229404.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
233,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941768475689869242.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
234,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941768475689869242.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601160242
235,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476041229404.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
236,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571768476097727957.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
237,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571768476097727957.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
238,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx191768475188890142.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
239,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571768476097727957.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
240,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx571768476097727957.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
241,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx461768475211220955.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
242,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768476305428428.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
243,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768476305428428.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
244,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768476305428428.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
245,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768476305428428.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
246,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476550103555.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
247,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476550103555.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
248,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476550103555.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
249,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476550103555.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
250,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181768476584358150.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
251,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181768476584358150.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
252,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181768476584358150.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
253,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181768476584358150.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
254,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476851610420.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190021
255,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476851610420.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
256,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476851610420.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
257,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx701768476851610420.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
258,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476875455273.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
259,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476875455273.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
260,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476875455273.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
261,PHK_345Y,PHK_345YJDF4,2026-01-23T12:11:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768476875455273.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
262,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx501768357348385941.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
263,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx501768357261649938.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
264,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx751768357290537805.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
265,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx551768358336621675.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601190029
266,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx251768357317838247.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601190029
267,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881768381071527040.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
268,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx761768358411728702.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
269,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx671768358430530842.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
270,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx121768357800728095.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,D202601190029
271,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx141768357829897638.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
272,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx931768357860670123.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
273,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx811768359082296136.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,D202601190029
274,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx761768358940006331.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
275,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx311768359937269138.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
276,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx331768360557037605.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
277,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181768360001867665.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
278,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx531768358975185618.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
279,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx331768360638043820.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
280,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx301768360681538253.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
281,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx401768363153268041.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
282,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx421768361134192093.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
283,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx211768376633465061.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
284,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx281768361100291566.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
285,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx641768363208384241.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
286,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx801768360093353811.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
287,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx901768376562729745.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
288,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx531768376687916158.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
289,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx321768363093609459.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
290,PHK_36X8,PHK_36X83VKB,2026-01-15T05:09:47,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx151768361211111877.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
291,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx151768480791540023.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
292,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx961768481084339253.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
293,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx131768480862163534.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
294,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx251768481091681262.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
295,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx911768481045735510.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
296,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx611768480763838007.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
297,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx261768481330245395.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
298,PHK_35LG,PHK_35LG33GV,2026-01-15T16:50:18,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx361768480550509388.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,
299,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx921768544701712201.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
300,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx231768544564861998.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
301,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx351768544845585191.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
302,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx561768544933180697.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
303,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx631768545424450046.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
304,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx321768544496545606.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
305,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx651768547511233891.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
306,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981768547322274785.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
307,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx371768545366222017.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,
308,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx711768545278437295.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
309,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx221768545450286123.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
310,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941768545206535034.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
311,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx431768549103113082.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,
312,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx911768545326490612.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
313,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981768545356836739.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
314,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx411768545474566266.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,
315,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx281768545235428881.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
316,PHO_34WR,PHO_34WRETUB,2026-01-16T07:40:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx881768545077806049.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
317,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx711768548888361703.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
318,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx911768549122238780.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
319,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx401768549014876595.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
320,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx101768549200323735.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
321,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx291768547371569949.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
322,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx201768547725158697.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
323,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx401768547701260399.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
324,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx221768549188615787.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
325,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771768547681755289.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
326,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx381768549156583601.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
327,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx431768547811360207.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,
328,PHK_36VH,PHK_36VHTQ39,2026-01-16T07:57:10,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951768547127837846.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
329,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx311768791572841946.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
330,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx791768791689181476.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
331,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx121768791563732352.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
332,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx431768792176661605.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,
333,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx551768791753042392.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
334,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx481768791465136566.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
335,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx471768791888178532.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
336,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx981768792109389360.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-3-pro-image-preview,场景,
337,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx391768792747785495.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
338,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx771768793026150751.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
339,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx591768792894506631.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
340,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx151768793048490510.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
341,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx151768792845818899.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
342,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx121768792932703746.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
343,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx661768803197042346.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
344,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx381768793340657768.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,
345,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx691768803924861795.jpeg,品牌BU,品牌BG,陈笑,"尺寸图...",gemini-3-pro-image-preview,尺寸图,
346,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx671768803331961600.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
347,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx181768793135611592.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
348,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx341768793378550456.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
349,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951768793312144305.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
350,PHK_36EJ,PHK_36EJUS3S,2026-01-20T02:34:02,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx951768803797547087.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
351,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx671768793268118038.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
352,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx971768794164285925.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
353,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx991768793352574479.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
354,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx751768793682945248.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,
355,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx741768793516002887.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
356,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx361768794270812087.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
357,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx911768794245652274.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
358,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx551768803186896405.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,
359,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx671768794320256934.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
360,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx221768794384769045.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
361,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx151768815146856073.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
362,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx661768794357736575.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
363,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx641768815040180741.jpeg,品牌BU,品牌BG,陈笑,"白底主图...",gemini-3-pro-image-preview,白底主图,
364,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx201768815117986439.jpeg,品牌BU,品牌BG,陈笑,"场景图...",gemini-3-pro-image-preview,场景图,
365,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx941768815443463685.jpeg,品牌BU,品牌BG,陈笑,"图...",gemini-2.5-flash-image,场景,
366,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx491768815235571151.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图,
367,PHK_367T,PHK_367TDBVM,2026-01-20T03:45:19,https://imageosscn.oss-cn-shenzhen.aliyuncs.com/starx/edith/nano_banana/sx411768815203371568.jpeg,品牌BU,品牌BG,陈笑,"细节图...",gemini-3-pro-image-preview,细节图`;

// 解析CSV函数
function parseCSV(text) {
    const lines = [];
    let currentLine = [];
    let currentVal = '';
    let inQuote = false;

    for(let i=0; i<text.length; i++) {
        let c = text[i];
        if(c === '"') { inQuote = !inQuote; }
        else if(c === ',' && !inQuote) {
            currentLine.push(currentVal);
            currentVal = '';
        } else if((c === '\n' || c === '\r') && !inQuote) {
            if(currentVal || currentLine.length > 0) {
                currentLine.push(currentVal);
                lines.push(currentLine);
            }
            currentLine = [];
            currentVal = '';
            if(c === '\r' && text[i+1] === '\n') i++;
        } else {
            currentVal += c;
        }
    }
    if(currentVal || currentLine.length > 0) { currentLine.push(currentVal); lines.push(currentLine); }

    // 跳过表头
    return lines.slice(1).map(row => {
        // 数据映射 (注意第12列是工单号)
        // 0:id, 1:SPU, 2:sku, 3:生成时间, 4:URL, 5:BU, 6:BG, 7:操作人, 8:提示词, 9:模型, 10:提示词分类, 11:工单号
        return {
            id: row[0],
            spu: row[1],
            sku: row[2],
            time: row[3],
            url: row[4],
            bu: row[5],
            bg: row[6],
            user: row[7],
            prompt: row[8] ? row[8].replace(/^"|"$/g, '') : '',
            model: row[9],
            type: row[10] ? row[10].trim() : '其他',
            orderId: row[11] ? row[11].trim() : '未知工单'
        };
    }).filter(item => item.id && item.url);
}

// 状态管理
let allData = parseCSV(rawData);
let currentMode = 'SPU'; // SPU, TIME, ORDER
let groups = {};

// 切换模式
function switchMode(mode, btn) {
    currentMode = mode;
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    updateGroups();
    renderSidebar();
    renderContent('all');
}

// 分组逻辑
function updateGroups() {
    groups = {};
    allData.forEach(item => {
        let mainKey = '';
        let subKey = '';

        if(currentMode === 'SPU') {
            mainKey = item.spu;
            subKey = item.sku;
        } else if(currentMode === 'TIME') {
            mainKey = item.time.split('T')[0];
            subKey = item.spu;
        } else if(currentMode === 'ORDER') {
            mainKey = item.orderId; // 按工单号分组
            subKey = item.spu;
        }

        if(!groups[mainKey]) groups[mainKey] = { count: 0, subs: {} };
        groups[mainKey].count++;

        if(!groups[mainKey].subs[subKey]) groups[mainKey].subs[subKey] = [];
        groups[mainKey].subs[subKey].push(item);
    });
}

// 渲染侧边栏
function renderSidebar() {
    const listEl = document.getElementById('sidebarList');
    listEl.innerHTML = '';

    const allDiv = document.createElement('div');
    allDiv.className = 'sidebar-item active';
    allDiv.innerHTML = `<span>全部</span><span class="count-tag">${allData.length}</span>`;
    allDiv.onclick = function() { highlightSidebar(this); renderContent('all'); };
    listEl.appendChild(allDiv);

    Object.keys(groups).sort().forEach(key => {
        const div = document.createElement('div');
        div.className = 'sidebar-item';
        div.innerHTML = `<span>${key}</span><span class="count-tag">${groups[key].count}</span>`;
        div.onclick = function() { highlightSidebar(this); renderContent(key); };
        listEl.appendChild(div);
    });
}

function highlightSidebar(el) {
    document.querySelectorAll('.sidebar-item').forEach(d => d.classList.remove('active'));
    el.classList.add('active');
}

// 渲染主内容
function renderContent(filterKey) {
    const container = document.getElementById('content');
    container.innerHTML = '';
    
    let displayKeys = (filterKey === 'all') ? Object.keys(groups).sort() : [filterKey];
    let totalCount = 0;

    const titleMap = { 'SPU': '按SPU查看', 'TIME': '按生成时间查看', 'ORDER': '按工单号查看' };
    document.getElementById('pageTitle').innerText = (filterKey === 'all') ? titleMap[currentMode] : filterKey;

    displayKeys.forEach(mainKey => {
        const group = groups[mainKey];
        if(!group) return;
        totalCount += group.count;

        const block = document.createElement('div');
        block.className = 'group-block';
        
        const header = document.createElement('div');
        header.className = 'group-header';
        header.innerHTML = `<span>${mainKey}</span><span class="group-total">${group.count}张</span>`;
        block.appendChild(header);

        Object.keys(group.subs).sort().forEach(subKey => {
            const items = group.subs[subKey];
            const subBlock = document.createElement('div');
            subBlock.className = 'sub-group-block';
            
            const subTitle = document.createElement('div');
            subTitle.className = 'sub-group-title';
            subTitle.innerText = subKey;
            subBlock.appendChild(subTitle);

            const grid = document.createElement('div');
            grid.className = 'grid';

            items.forEach(item => {
                const card = document.createElement('div');
                card.className = 'card';
                
                // 处理分类标签显示
                let displayType = item.type.replace(/[^\u4e00-\u9fa5a-zA-Z0-9]/g, '');
                if(!displayType) displayType = "素材";
                
                // 格式化时间
                let timeStr = item.time.split('T')[0];

                // 卡片底部内容：提示词分类 BG BU 操作人 时间
                card.innerHTML = `
                    <div class="card-img-wrapper">
                        <img class="card-img" src="${item.url}" loading="lazy">
                    </div>
                    <div class="card-body">
                        <div class="tag-row"><span class="type-tag">${displayType}</span></div>
                        <div class="info-row">
                            <span>BG: <span class="info-val">${item.bg}</span></span>
                            <span>BU: <span class="info-val">${item.bu}</span></span>
                        </div>
                        <div class="info-row">
                            <span>User: <span class="info-val">${item.user}</span></span>
                            <span>Date: <span class="info-val">${timeStr}</span></span>
                        </div>
                    </div>
                `;
                card.onclick = () => openModal(item);
                grid.appendChild(card);
            });

            subBlock.appendChild(grid);
            block.appendChild(subBlock);
        });

        container.appendChild(block);
    });

    document.getElementById('pageCount').innerText = `当前显示 ${totalCount} 张图片`;
}

// 弹窗逻辑
const modal = document.getElementById("myModal");
function openModal(item) {
    document.getElementById('mImg').src = item.url;
    // 填充所有字段
    document.getElementById('mID').innerText = item.id;
    document.getElementById('mSPU').innerText = item.spu;
    document.getElementById('mSKU').innerText = item.sku;
    document.getElementById('mOrder').innerText = item.orderId;
    
    document.getElementById('mType').innerText = item.type;
    document.getElementById('mBU').innerText = item.bu;
    document.getElementById('mBG').innerText = item.bg;
    document.getElementById('mUser').innerText = item.user;
    document.getElementById('mTime').innerText = item.time.replace('T', ' ');
    document.getElementById('mModel').innerText = item.model;
    
    document.getElementById('mURL').href = item.url;
    document.getElementById('mPrompt').innerText = item.prompt;
    
    modal.style.display = "flex";
}
function closeModal() { modal.style.display = "none"; }
window.onclick = function(e) { if(e.target == modal) closeModal(); }

// 初始化
updateGroups();
renderSidebar();
renderContent('all');
</script>
</body>
</html>
