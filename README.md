<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Free online tools for image compression, document conversion, and PDF creation. Convert Word to PDF, compress images, create PDF from images, and scan documents.">
    <meta name="keywords" content="Image Compressor, Word to PDF, PDF Converter, Scan to PDF, Image to PDF">
    <title>Online File Tools - Image & Document Converter</title>
    <style>
        :root {
            --primary: #6C63FF;
            --secondary: #4A90E2;
            --bg: #f8f9fa;
            --text: #2d3436;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', sans-serif;
        }

        body {
            background: var(--bg);
            color: var(--text);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .tool-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            overflow-x: auto;
        }

        .tab-btn {
            background: #fff;
            border: none;
            padding: 12px 25px;
            border-radius: 8px;
            cursor: pointer;
            transition: 0.3s;
            font-weight: 500;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .tab-btn.active {
            background: var(--primary);
            color: white;
        }

        .tool-section {
            display: none;
            background: white;
            padding: 25px;
            border-radius: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .tool-section.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Image Compressor Styles */
        .file-upload {
            border: 2px dashed #ddd;
            padding: 30px;
            text-align: center;
            margin: 20px 0;
            border-radius: 12px;
            cursor: pointer;
        }

        .preview-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }

        .image-card {
            position: relative;
            border-radius: 8px;
            overflow: hidden;
        }

        .image-preview {
            width: 100%;
            height: 120px;
            object-fit: cover;
        }

        .file-size {
            position: absolute;
            bottom: 0;
            background: rgba(0,0,0,0.7);
            color: white;
            width: 100%;
            padding: 5px;
            font-size: 12px;
            text-align: center;
        }

        .compression-controls {
            margin: 20px 0;
        }

        .slider-container {
            margin: 15px 0;
        }

        .compression-slider {
            width: 100%;
            height: 8px;
            accent-color: var(--primary);
        }

        .output-actions {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }

        .action-btn {
            background: var(--primary);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            flex: 1;
            transition: 0.3s;
        }

        .action-btn:hover {
            opacity: 0.9;
        }

        /* Word to PDF Styles */
        .file-list {
            list-style: none;
            margin: 15px 0;
        }

        .file-item {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            background: #f8f9fa;
            margin: 5px 0;
            border-radius: 8px;
        }

        .progress-bar {
            height: 8px;
            background: #eee;
            border-radius: 4px;
            overflow: hidden;
            margin: 15px 0;
        }

        .progress {
            height: 100%;
            background: var(--primary);
            transition: width 0.3s ease;
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .tab-btn {
                padding: 10px 15px;
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 style="text-align: center; margin: 30px 0; color: var(--primary);">Online File Tools</h1>
        
        <div class="tool-tabs">
            <button class="tab-btn active" onclick="showTool('image-compressor')">Image Compressor</button>
            <button class="tab-btn" onclick="showTool('word-pdf')">Word to PDF</button>
            <button class="tab-btn" onclick="showTool('scan-pdf')">Scan to PDF</button>
            <button class="tab-btn" onclick="showTool('image-pdf')">Image to PDF</button>
        </div>

        <!-- Image Compressor -->
        <section id="tool
        image-compressor" class="tool-section active">
            <h2>Image Compressor</h2>
            <div class="file-upload" onclick="document.getElementById('image-upload').click()">
                Click to Select Images
                <input type="file" id="image-upload" accept="image/*" multiple hidden>
            </div>
            <div class="preview-grid"></div>
            <div class="compression-controls">
                <div class="slider-container">
                    <label>Compression Level:</label>
                    <input type="range" class="compression-slider" min="0" max="2" step="1" value="1">
                    <div class="slider-labels">
                        <span>Low</span>
                        <span>Medium</span>
                        <span>High</span>
                    </div>
                </div>
                <div class="size-estimate">Estimated Size: -</div>
            </div>
            <button class="action-btn" onclick="compressImages()">Compress Now</button>
            <div class="output-actions" style="display: none;">
                <button class="action-btn">Save</button>
                <button class="action-btn">Share</button>
            </div>
        </section>

        <!-- Word to PDF Converter -->
        <section id="word-pdf" class="tool-section">
            <h2>Word to PDF Converter</h2>
            <div class="file-upload" onclick="document.getElementById('doc-upload').click()">
                Upload DOC/DOCX Files
                <input type="file" id="doc-upload" accept=".doc,.docx" multiple hidden>
            </div>
            <ul class="file-list"></ul>
            <button class="action-btn" onclick="convertToPDF()">Convert to PDF</button>
            <div class="progress-bar">
                <div class="progress" style="width: 0%"></div>
            </div>
            <div class="output-actions" style="display: none;">
                <button class="action-btn">Open</button>
                <button class="action-btn">Save</button>
                <button class="action-btn">Share</button>
            </div>
        </section>

        <!-- Other tool sections... -->
    </div>

    <script>
        function showTool(toolId) {
            document.querySelectorAll('.tool-section').forEach(section => {
                section.classList.remove('active');
            });
            document.getElementById(toolId).classList.add('active');
            
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
        }

        // Image Compressor Logic
        document.getElementById('image-upload').addEventListener('change', function(e) {
            const previewGrid = document.querySelector('#image-compressor .preview-grid');
            previewGrid.innerHTML = '';
            
            Array.from(e.target.files).forEach(file => {
                const reader = new FileReader();
                reader.onload = () => {
                    const card = document.createElement('div');
                    card.className = 'image-card';
                    card.innerHTML = `
                        <img src="${reader.result}" class="image-preview">
                        <div class="file-size">${formatSize(file.size)}</div>
                    `;
                    previewGrid.appendChild(card);
                };
                reader.readAsDataURL(file);
            });
        });

        function formatSize(bytes) {
            const sizes = ['Bytes', 'KB', 'MB', 'GB'];
            if (bytes === 0) return '0 Bytes';
            const i = Math.floor(Math.log(bytes) / Math.log(1024));
            return parseFloat((bytes / Math.pow(1024, i)).toFixed(2)) + ' ' + sizes[i];
        }

        function compressImages() {
            const btn = document.querySelector('#image-compressor .action-btn');
            btn.disabled = true;
            btn.textContent = 'Compressing...';
            
            setTimeout(() => {
                btn.textContent = 'Compression Complete!';
                document.querySelector('#image-compressor .output-actions').style.display = 'flex';
                btn.disabled = false;
            }, 2000);
        }

        // Word to PDF Logic
        document.getElementById('doc-upload').addEventListener('change', function(e) {
            const fileList = document.querySelector('#word-pdf .file-list');
            fileList.innerHTML = '';
            
            Array.from(e.target.files).forEach(file => {
                const li = document.createElement('li');
                li.className = 'file-item';
                li.innerHTML = `
                    <span>${file.name}</span>
                    <span>${formatSize(file.size)}</span>
                `;
                fileList.appendChild(li);
            });
        });

        function convertToPDF() {
            const progress = document.querySelector('#word-pdf .progress');
            let width = 0;
            const interval = setInterval(() => {
                if (width >= 100) {
                    clearInterval(interval);
                    document.querySelector('#word-pdf .output-actions').style.display = 'flex';
                } else {
                    width += 10;
                    progress.style.width = width + '%';
                }
            }, 300);
        }
    </script>
</body>
</html>
