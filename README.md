<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GoTech - Guia Local de Profissionais</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar">
        <div class="container">
            <div class="logo" onclick="goHome()">
                <h1>🏢 GoTech</h1>
            </div>
            <ul class="nav-links">
                <li><a onclick="showHome()">Home</a></li>
                <li><a onclick="showServicos()">Serviços</a></li>
                <li><a onclick="showCadastro()">Cadastro</a></li>
            </ul>
        </div>
    </nav>

    <!-- HOME SECTION -->
    <section class="hero" id="secHome">
        <div class="hero-content">
            <h1>Encontre os Melhores Profissionais da Sua Cidade</h1>
            <p>Conecte-se com encanadores, eletricistas, pintores, confeiteiros, fotógrafos e muito mais. Tudo em um único lugar!</p>
            <img src="https://images.unsplash.com/photo-1552664730-d307ca884978?w=600&h=400&fit=crop" alt="Profissionais trabalhando" class="hero-image">
            <button class="btn-primary" onclick="showServicos()">Explorar Serviços</button>
        </div>
    </section>

    <!-- SERVIÇOS SECTION -->
    <section class="servicos-section" id="secServicos" style="display: none;">
        <div class="container">
            <button class="btn-back" onclick="showHome()">← Voltar</button>
            <h2>🔧 Escolha um Serviço</h2>
            <p style="text-align: center; color: var(--text-light); margin-bottom: 40px;">Clique em um serviço para ver os profissionais disponíveis</p>
            
            <div class="services-grid" id="servicesGrid">
                <!-- Cards de serviços gerados pelo JavaScript -->
            </div>
        </div>
    </section>

    <!-- PROFISSIONAIS SECTION -->
    <section class="profissionais-section" id="secProfissionais" style="display: none;">
        <div class="container">
            <button class="btn-back" onclick="showServicos()">← Voltar</button>
            <h2 id="categoryTitle"></h2>
            <p id="categoryDescription" style="text-align: center; color: var(--text-light); margin-bottom: 30px;"></p>
            
            <div class="search-container">
                <input type="text" id="searchInput" class="search-input" placeholder="Busque por nome do profissional...">
            </div>

            <div class="professionals-grid" id="professionalsGrid">
                <!-- Cards gerados pelo JavaScript -->
            </div>
        </div>
    </section>

    <!-- CADASTRO SECTION -->
    <section class="cadastro-section" id="secCadastro" style="display: none;">
        <div class="container">
            <button class="btn-back" onclick="showHome()">← Voltar</button>
            <div class="form-container">
                <h2>📝 Cadastre-se como Profissional</h2>
                <p>Expanda seu negócio e conecte-se com mais clientes</p>
                
                <form id="registrationForm">
                    <div class="form-group">
                        <label for="name">Nome Completo *</label>
                        <input type="text" id="name" name="name" placeholder="Seu nome completo" required>
                        <small>Mínimo 3 caracteres</small>
                        <span class="error-message" id="nameError"></span>
                    </div>

                    <div class="form-group">
                        <label for="category">Categoria/Profissão *</label>
                        <select id="category" name="category" required>
                            <option value="">Selecione uma profissão</option>
                            <option value="encanador">🚰 Encanador</option>
                            <option value="eletricista">⚡ Eletricista</option>
                            <option value="pintor">🎨 Pintor</option>
                            <option value="confeiteiro">🍰 Confeiteiro</option>
                            <option value="fotografo">📸 Fotógrafo</option>
                            <option value="designer">💻 Designer</option>
                            <option value="mecanico">🔧 Mecânico</option>
                        </select>
                        <span class="error-message" id="categoryError"></span>
                    </div>

                    <div class="form-group">
                        <label for="description">Descrição de Serviços</label>
                        <textarea id="description" name="description" rows="4" placeholder="Descreva seus serviços..."></textarea>
                        <small>Máximo 200 caracteres</small>
                    </div>

                    <div class="form-group">
                        <label for="whatsapp">WhatsApp *</label>
                        <input type="tel" id="whatsapp" name="whatsapp" placeholder="(11) 99999-9999" required>
                        <small>Formato: (XX) 9XXXX-XXXX</small>
                        <span class="error-message" id="whatsappError"></span>
                    </div>

                    <div class="form-group">
                        <label for="city">Cidade *</label>
                        <input type="text" id="city" name="city" placeholder="Sua cidade" required>
                        <span class="error-message" id="cityError"></span>
                    </div>

                    <!-- Upload de Foto -->
                    <div class="form-group">
                        <label for="photo">Foto do Perfil *</label>
                        <div class="photo-upload-buttons" id="photoUploadButtons"></div>
                        <div class="photo-upload-area" id="photoUploadArea">
                            <input type="file" id="photo" name="photo" accept="image/*" required style="display: none;">
                            <div class="upload-placeholder">
                                <div style="font-size: 40px; margin-bottom: 10px;">📷</div>
                                <p>Clique ou arraste uma foto aqui</p>
                                <small>PNG, JPG até 5MB</small>
                            </div>
                        </div>
                        <span class="error-message" id="photoError"></span>
                        
                        <!-- Preview da Foto -->
                        <div id="photoPreview" style="display: none; margin-top: 15px;">
                            <p style="font-weight: 600; margin-bottom: 10px;">Preview:</p>
                            <img id="previewImage" style="max-width: 200px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);">
                        </div>
                    </div>

                    <button type="submit" class="btn-primary" style="width: 100%; margin-top: 10px;">Cadastrar</button>
                </form>
            </div>
        </div>
    </section>

    <!-- Modal de Avaliação -->
    <div id="reviewModal" class="modal" style="display: none;">
        <div class="modal-content">
            <span class="close" onclick="closeReviewModal()">&times;</span>
            <h2>⭐ Avaliar Profissional</h2>
            <p id="professionalNameReview"></p>
            
            <div class="rating-stars">
                <span class="star" onclick="setRating(1)">⭐</span>
                <span class="star" onclick="setRating(2)">⭐</span>
                <span class="star" onclick="setRating(3)">⭐</span>
                <span class="star" onclick="setRating(4)">⭐</span>
                <span class="star" onclick="setRating(5)">⭐</span>
            </div>
            <p id="ratingText">Clique nas estrelas para avaliar</p>

            <div class="form-group">
                <label for="reviewerName">Seu Nome</label>
                <input type="text" id="reviewerName" placeholder="Seu nome">
            </div>

            <div class="form-group">
                <label for="reviewComment">Seu Comentário</label>
                <textarea id="reviewComment" rows="4" placeholder="Deixe seu comentário..."></textarea>
            </div>

            <button class="btn-primary" onclick="submitReview()" style="width: 100%;">Enviar Avaliação</button>
        </div>
    </div>

    <!-- Footer -->
    <footer class="footer">
        <div class="container">
            <p>&copy; 2026 GoTech - Guia Local de Profissionais. Todos os direitos reservados.</p>
            <p>📧 Email: <strong>contato@gotech.com</strong></p>
            <p>🔗 Reclamações: <a href="https://www.reclameaqui.com.br" target="_blank">Clique aqui para acessar Reclame Aqui!</a></p>
        </div>
    </footer>

    <script src="script.js"></script>
</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

:root {
    --primary-color: #6366f1;
    --secondary-color: #ec4899;
    --dark-bg: #0f172a;
    --light-bg: #f8fafc;
    --card-bg: #ffffff;
    --text-dark: #1e293b;
    --text-light: #64748b;
    --border-color: #e2e8f0;
    --success-color: #10b981;
    --error-color: #ef4444;
}

html {
    scroll-behavior: smooth;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    line-height: 1.6;
    color: var(--text-dark);
    background-color: var(--light-bg);
}

.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* Navigation */
.navbar {
    background: white;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    position: sticky;
    top: 0;
    z-index: 100;
}

.navbar .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 20px;
}

.logo h1 {
    font-size: 24px;
    color: var(--primary-color);
    cursor: pointer;
    transition: transform 0.3s ease;
}

.logo h1:hover {
    transform: scale(1.05);
}

.nav-links {
    display: flex;
    list-style: none;
    gap: 30px;
    align-items: center;
}

.nav-links a {
    text-decoration: none;
    color: var(--text-dark);
    font-weight: 500;
    transition: color 0.3s ease;
    cursor: pointer;
}

.nav-links a:hover {
    color: var(--primary-color);
}

/* Hero Section */
.hero {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 30px;
    padding: 80px 20px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    min-height: 100vh;
    text-align: center;
}

.hero-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 30px;
}

.hero-content h1 {
    font-size: 48px;
    line-height: 1.2;
    max-width: 600px;
}

.hero-content p {
    font-size: 18px;
    opacity: 0.9;
    max-width: 600px;
}

.hero-image {
    width: 100%;
    max-width: 600px;
    height: auto;
    border-radius: 16px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    animation: fadeIn 0.8s ease-out;
}

/* Serviços Section */
.servicos-section {
    padding: 60px 20px;
    background: white;
    min-height: 100vh;
}

.servicos-section h2 {
    font-size: 32px;
    margin-bottom: 15px;
    text-align: center;
}

/* Services Grid */
.services-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 30px;
    background: white;
    padding: 0;
}

.service-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
    transition: all 0.3s ease;
    padding: 25px;
    border-radius: 12px;
    background: var(--card-bg);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.service-card:hover {
    transform: translateY(-12px);
    box-shadow: 0 15px 30px rgba(99, 102, 241, 0.2);
}

.service-image {
    width: 140px;
    height: 140px;
    object-fit: cover;
    border-radius: 12px;
    margin-bottom: 15px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.service-name {
    font-size: 20px;
    font-weight: 700;
    color: var(--text-dark);
    text-align: center;
    margin-bottom: 8px;
}

.service-count {
    font-size: 13px;
    color: var(--primary-color);
    margin-top: 8px;
    font-weight: 600;
}

/* Buttons */
.btn-primary {
    background: var(--secondary-color);
    color: white;
    border: none;
    padding: 14px 40px;
    font-size: 16px;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-weight: 600;
}

.btn-primary:hover {
    background: #be185d;
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(236, 72, 153, 0.3);
}

.btn-back {
    background: var(--border-color);
    color: var(--text-dark);
    border: none;
    padding: 10px 20px;
    border-radius: 6px;
    cursor: pointer;
    font-weight: 600;
    margin-bottom: 20px;
    transition: all 0.3s ease;
}

.btn-back:hover {
    background: var(--primary-color);
    color: white;
}

.btn-whatsapp {
    background: #25d366;
    color: white;
    border: none;
    padding: 10px 20px;
    font-size: 14px;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-weight: 600;
}

.btn-whatsapp:hover {
    background: #20ba5a;
    transform: scale(1.05);
}

/* Search Section */
.profissionais-section {
    padding: 60px 20px;
    background: white;
    min-height: 100vh;
}

.profissionais-section h2 {
    font-size: 32px;
    margin-bottom: 10px;
    text-align: center;
}

.search-container {
    margin-bottom: 40px;
}

.search-input {
    width: 100%;
    padding: 16px 20px;
    font-size: 16px;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    margin-bottom: 20px;
    transition: border-color 0.3s ease;
}

.search-input:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

/* Professionals Grid */
.professionals-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 30px;
}

/* Professional Card */
.professional-card {
    background: var(--card-bg);
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
    animation: fadeIn 0.5s ease-out;
}

.professional-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
}

.card-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.card-content {
    padding: 20px;
}

.card-category {
    display: inline-block;
    background: rgba(99, 102, 241, 0.1);
    color: var(--primary-color);
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 12px;
    font-weight: 600;
    margin-bottom: 12px;
}

.card-name {
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 8px;
    color: var(--text-dark);
}

.card-city {
    font-size: 13px;
    color: var(--text-light);
    margin-bottom: 12px;
}

.card-description {
    color: var(--text-light);
    font-size: 14px;
    margin-bottom: 20px;
    line-height: 1.5;
}

.card-rating {
    font-size: 14px;
    color: var(--primary-color);
    margin-bottom: 15px;
    font-weight: 600;
}

.card-reviews {
    background: #f8f9fa;
    padding: 15px;
    border-radius: 8px;
    margin-bottom: 15px;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.3s ease;
}

.card-reviews.expanded {
    max-height: 500px;
}

.review-item {
    margin-bottom: 12px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--border-color);
}

.review-item:last-child {
    border-bottom: none;
    margin-bottom: 0;
    padding-bottom: 0;
}

.review-author {
    font-weight: 600;
    color: var(--text-dark);
    font-size: 13px;
}

.review-rating {
    color: #ffc107;
    font-size: 12px;
}

.review-text {
    font-size: 13px;
    color: var(--text-light);
    margin-top: 4px;
}

.card-footer {
    display: flex;
    gap: 10px;
}

.card-whatsapp {
    flex: 1;
    background: #25d366;
    color: white;
    border: none;
    padding: 12px 16px;
    border-radius: 8px;
    cursor: pointer;
    font-weight: 600;
    transition: all 0.3s ease;
    font-size: 14px;
}

.card-whatsapp:hover {
    background: #20ba5a;
    transform: scale(1.05);
}

.card-rate-btn {
    flex: 1;
    background: var(--primary-color);
    color: white;
    border: none;
    padding: 12px 16px;
    border-radius: 8px;
    cursor: pointer;
    font-weight: 600;
    transition: all 0.3s ease;
    font-size: 14px;
}

.card-rate-btn:hover {
    background: #4f46e5;
    transform: scale(1.05);
}

.card-reviews-toggle {
    background: var(--border-color);
    color: var(--text-dark);
    border: none;
    padding: 8px 12px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 12px;
    transition: all 0.3s ease;
    width: 100%;
    margin-bottom: 10px;
}

.card-reviews-toggle:hover {
    background: var(--primary-color);
    color: white;
}

/* Cadastro Section */
.cadastro-section {
    padding: 60px 20px;
    background: white;
    min-height: 100vh;
}

.form-container {
    max-width: 500px;
    margin: 0 auto;
}

.form-container h2 {
    font-size: 32px;
    margin-bottom: 10px;
    text-align: center;
}

.form-container p {
    color: var(--text-light);
    margin-bottom: 30px;
    text-align: center;
}

.form-group {
    margin-bottom: 20px;
}

.form-group label {
    display: block;
    font-weight: 600;
    margin-bottom: 8px;
    color: var(--text-dark);
}

.form-group input,
.form-group select,
.form-group textarea {
    width: 100%;
    padding: 12px;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    font-size: 14px;
    font-family: inherit;
    transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.1);
}

.form-group small {
    display: block;
    margin-top: 6px;
    color: var(--text-light);
    font-size: 12px;
}

.error-message {
    display: block;
    color: var(--error-color);
    font-size: 12px;
    margin-top: 4px;
}

.form-group input.error,
.form-group select.error,
.form-group textarea.error {
    border-color: var(--error-color);
}

/* Photo Upload */
.photo-upload-area {
    position: relative;
    border: 2px dashed var(--border-color);
    border-radius: 8px;
    padding: 30px;
    text-align: center;
    cursor: pointer;
    transition: all 0.3s ease;
    background: var(--light-bg);
}

.photo-upload-area:hover {
    border-color: var(--primary-color);
    background: rgba(99, 102, 241, 0.05);
}

.photo-upload-area input[type="file"] {
    display: none;
}

.upload-placeholder {
    pointer-events: none;
    color: var(--text-light);
}

.photo-upload-area p {
    font-weight: 600;
    margin: 10px 0;
    color: var(--text-dark);
}

.photo-upload-area small {
    color: var(--text-light);
}

/* Modal */
.modal {
    display: none;
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.6);
    animation: fadeIn 0.3s ease;
}

.modal-content {
    background-color: white;
    margin: 5% auto;
    padding: 30px;
    border-radius: 12px;
    width: 90%;
    max-width: 500px;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
}

.close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
    cursor: pointer;
    transition: color 0.3s ease;
}

.close:hover {
    color: #000;
}

.modal h2 {
    margin-bottom: 20px;
    color: var(--text-dark);
}

.modal p {
    margin-bottom: 20px;
    color: var(--text-light);
}

.rating-stars {
    display: flex;
    gap: 15px;
    margin-bottom: 20px;
    font-size: 40px;
}

.star {
    cursor: pointer;
    transition: transform 0.2s ease;
    opacity: 0.3;
}

.star:hover {
    transform: scale(1.2);
    opacity: 1;
}

.star.active {
    opacity: 1;
}

#ratingText {
    margin-bottom: 20px !important;
    color: var(--primary-color);
    font-weight: 600;
}

/* Footer */
.footer {
    background: var(--dark-bg);
    color: white;
    padding: 40px 20px;
    text-align: center;
}

.footer p {
    margin: 10px 0;
    line-height: 1.8;
}

.footer a {
    color: #ec4899;
    text-decoration: none;
    font-weight: 600;
    transition: color 0.3s ease;
}

.footer a:hover {
    color: #be185d;
    text-decoration: underline;
}

/* Animations */
@keyframes fadeIn {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* Responsive */
@media (max-width: 768px) {
    .hero {
        padding: 60px 20px;
        min-height: auto;
    }

    .hero-content h1 {
        font-size: 32px;
    }

    .hero-content p {
        font-size: 16px;
    }

    .services-grid {
        grid-template-columns: repeat(2, 1fr);
    }

    .nav-links {
        gap: 15px;
    }

    .nav-links a {
        font-size: 14px;
    }

    .professionals-grid {
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    }

    .modal-content {
        width: 95%;
        margin: 20% auto;
    }
}

@media (max-width: 480px) {
    .logo h1 {
        font-size: 18px;
    }

    .nav-links {
        gap: 10px;
    }

    .nav-links a {
        font-size: 12px;
    }

    .hero-content h1 {
        font-size: 24px;
    }

    .hero-content p {
        font-size: 14px;
    }

    .services-grid {
        grid-template-columns: 1fr;
    }

    .professionals-grid {
        grid-template-columns: 1fr;
    }

    .modal-content {
        margin: 40% auto;
        padding: 20px;
    }

    .rating-stars {
        font-size: 30px;
        gap: 10px;
    }
}
// Serviços disponíveis
const services = [
    {
        id: 'encanador',
        name: '🚰 Encanador',
        emoji: '🚰',
        image: 'https://images.unsplash.com/photo-1584622614875-2953067881c7?w=400&h=400&fit=crop',
        description: 'Profissionais para instalação e manutenção de encanamento'
    },
    {
        id: 'eletricista',
        name: '⚡ Eletricista',
        emoji: '⚡',
        image: 'https://images.unsplash.com/photo-1581092916550-e323be2ae537?w=400&h=400&fit=crop',
        description: 'Especialistas em instalações e reparos elétricos'
    },
    {
        id: 'pintor',
        name: '🎨 Pintor',
        emoji: '🎨',
        image: 'https://images.unsplash.com/photo-1584611223722-9a9b86b481c0?w=400&h=400&fit=crop',
        description: 'Profissionais de pintura e acabamento'
    },
    {
        id: 'confeiteiro',
        name: '🍰 Confeiteiro',
        emoji: '🍰',
        image: 'https://images.unsplash.com/photo-1578985545062-69928b1d9587?w=400&h=400&fit=crop',
        description: 'Confeiteiros para eventos e celebrações'
    },
    {
        id: 'fotografo',
        name: '📸 Fotógrafo',
        emoji: '📸',
        image: 'https://images.unsplash.com/photo-1502920917128-1aa500764cbd?w=400&h=400&fit=crop',
        description: 'Fotógrafos profissionais para seus momentos especiais'
    },
    {
        id: 'designer',
        name: '💻 Designer',
        emoji: '💻',
        image: 'https://images.unsplash.com/photo-1561070791-2526d30994b5?w=400&h=400&fit=crop',
        description: 'Designers criativos para seus projetos'
    },
    {
        id: 'mecanico',
        name: '🔧 Mecânico',
        emoji: '🔧',
        image: 'https://images.unsplash.com/photo-1487573883260-228e8e46da4a?w=400&h=400&fit=crop',
        description: 'Mecânicos especializados em manutenção veicular'
    }
];
// Serviços disponíveis


// ============================================
// NAVEGAÇÃO
// ============================================

function showHome() {
    hideAllSections();
    document.getElementById('secHome').style.display = 'block';
    window.scrollTo(0, 0);
}

function showServicos() {
    hideAllSections();
    document.getElementById('secServicos').style.display = 'block';
    renderServices();
    window.scrollTo(0, 0);
}

function showCadastro() {
    hideAllSections();
    document.getElementById('secCadastro').style.display = 'block';
    window.scrollTo(0, 0);
}

function goHome() {
    showHome();
}

function hideAllSections() {
    document.getElementById('secHome').style.display = 'none';
    document.getElementById('secServicos').style.display = 'none';
    document.getElementById('secProfissionais').style.display = 'none';
    document.getElementById('secCadastro').style.display = 'none';
}

// ============================================
// INICIALIZAÇÃO
// ============================================

document.addEventListener('DOMContentLoaded', function() {
    loadDataFromStorage();
    setupForm();
    setupPhotoUpload();
    setupSearch();
});

// ============================================
// LOCALSTORAGE
// ============================================

function loadDataFromStorage() {
    const saved = localStorage.getItem('professionals');
    if (saved) {
        professionals = JSON.parse(saved);
    }
}

function saveDataToStorage() {
    localStorage.setItem('professionals', JSON.stringify(professionals));
}

// ============================================
// SERVIÇOS
// ============================================

function renderServices() {
    const grid = document.getElementById('servicesGrid');
    grid.innerHTML = '';
    
    services.forEach(service => {
        const count = professionals.filter(p => p.category === service.id).length;
        
        const card = document.createElement('div');
        card.className = 'service-card';
        card.onclick = () => openServiceCategory(service.id, service.name);
        
        card.innerHTML = `
            <img src="${service.image}" alt="${service.name}" class="service-image">
            <div class="service-name">${service.name}</div>
            <div class="service-count">${count} profissional${count !== 1 ? 'is' : ''}</div>
        `;
        
        grid.appendChild(card);
    });
}

function openServiceCategory(categoryId, categoryName) {
    currentCategory = categoryId;
    document.getElementById('categoryTitle').textContent = categoryName;
    
    const service = services.find(s => s.id === categoryId);
    document.getElementById('categoryDescription').textContent = service.description;
    
    hideAllSections();
    document.getElementById('secProfissionais').style.display = 'block';
    renderCategoryProfessionals();
    document.getElementById('searchInput').value = '';
    window.scrollTo(0, 0);
}

// ============================================
// PROFISSIONAIS
// ============================================

function renderCategoryProfessionals() {
    const grid = document.getElementById('professionalsGrid');
    grid.innerHTML = '';
    
    let filtered = professionals.filter(p => p.category === currentCategory);
    
    // Ordenar por melhor avaliação
    filtered.sort((a, b) => {
        const avgA = a.reviews.length > 0 ? a.reviews.reduce((sum, r) => sum + r.rating, 0) / a.reviews.length : 0;
        const avgB = b.reviews.length > 0 ? b.reviews.reduce((sum, r) => sum + r.rating, 0) / b.reviews.length : 0;
        return avgB - avgA;
    });
    
    // Aplicar busca
    const search = document.getElementById('searchInput').value.toLowerCase();
    if (search) {
        filtered = filtered.filter(p => 
            p.name.toLowerCase().includes(search) || 
            p.description.toLowerCase().includes(search)
        );
    }
    
    if (filtered.length === 0) {
        grid.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: var(--text-light); padding: 40px;">Nenhum profissional encontrado.</p>';
        return;
    }
    
    filtered.forEach(prof => {
        const card = document.createElement('div');
        card.className = 'professional-card';
        
        const avgRating = prof.reviews.length > 0 
            ? (prof.reviews.reduce((sum, r) => sum + r.rating, 0) / prof.reviews.length).toFixed(1)
            : 'Sem avaliações';
        
        const ratingText = prof.reviews.length > 0 
            ? `⭐ ${avgRating} (${prof.reviews.length} ${prof.reviews.length === 1 ? 'avaliação' : 'avaliações'})`
            : 'Sem avaliações ainda';
        
        card.innerHTML = `
            <img src="${prof.photo}" alt="${prof.name}" class="card-image">
            <div class="card-content">
                <span class="card-category">${prof.category}</span>
                <h3 class="card-name">${prof.name}</h3>
                <p class="card-city">📍 ${prof.city}</p>
                <p class="card-description">${prof.description}</p>
                <div class="card-rating">${ratingText}</div>
                
                <div class="card-reviews" id="reviews-${prof.id}">
                    ${prof.reviews.map(review => `
                        <div class="review-item">
                            <div class="review-author">${review.author}</div>
                            <div class="review-rating">${'⭐'.repeat(review.rating)}</div>
                            <div class="review-text">${review.comment}</div>
                        </div>
                    `).join('')}
                </div>
                
                ${prof.reviews.length > 0 ? `
                    <button class="card-reviews-toggle" onclick="toggleReviews(${prof.id})">Ver Avaliações</button>
                ` : ''}
                
                <div class="card-footer">
                    <button class="card-whatsapp" onclick="openWhatsApp('${prof.whatsapp}', '${prof.name}')">💬 WhatsApp</button>
                    <button class="card-rate-btn" onclick="openReviewModal(${prof.id}, '${prof.name}')">⭐ Avaliar</button>
                </div>
            </div>
        `;
        
        grid.appendChild(card);
    });
}

function toggleReviews(profId) {
    const reviewsDiv = document.getElementById(`reviews-${profId}`);
    const button = event.target;
    
    reviewsDiv.classList.toggle('expanded');
    button.textContent = reviewsDiv.classList.contains('expanded') ? 'Ocultar Avaliações' : 'Ver Avaliações';
}

function openWhatsApp(whatsapp, name) {
    const message = `Olá ${name}, gostaria de conhecer mais sobre seus serviços!`;
    const whatsappNumber = whatsapp.replace(/[^\d]/g, '');
    const url = `https://wa.me/${whatsappNumber}?text=${encodeURIComponent(message)}`;
    window.open(url, '_blank');
}

function setupSearch() {
    const searchInput = document.getElementById('searchInput');
    if (searchInput) {
        searchInput.addEventListener('input', () => {
            renderCategoryProfessionals();
        });
    }
}

// ============================================
// AVALIAÇÕES
// ============================================

function openReviewModal(profId, profName) {
    currentRatingProfessional = profId;
    currentRating = 0;
    
    document.getElementById('reviewModal').style.display = 'block';
    document.getElementById('professionalNameReview').textContent = `Avaliar: ${profName}`;
    document.getElementById('ratingText').textContent = 'Clique nas estrelas para avaliar';
    document.getElementById('reviewerName').value = '';
    document.getElementById('reviewComment').value = '';
    
    resetStars();
}

function closeReviewModal() {
    document.getElementById('reviewModal').style.display = 'none';
}

function setRating(rating) {
    currentRating = rating;
    updateStars();
    document.getElementById('ratingText').textContent = `Você selecionou ${rating} estrela${rating > 1 ? 's' : ''}`;
}

function updateStars() {
    const stars = document.querySelectorAll('.star');
    stars.forEach((star, index) => {
        if (index < currentRating) {
            star.classList.add('active');
        } else {
            star.classList.remove('active');
        }
    });
}

function resetStars() {
    document.querySelectorAll('.star').forEach(star => {
        star.classList.remove('active');
    });
}

function submitReview() {
    const name = document.getElementById('reviewerName').value.trim();
    const comment = document.getElementById('reviewComment').value.trim();
    
    if (!name) {
        alert('Por favor, digite seu nome');
        return;
    }
    
    if (currentRating === 0) {
        alert('Por favor, selecione uma classificação');
        return;
    }
    
    if (!comment) {
        alert('Por favor, deixe um comentário');
        return;
    }
    
    const prof = professionals.find(p => p.id === currentRatingProfessional);
    if (prof) {
        prof.reviews.push({
            author: name,
            rating: currentRating,
            comment: comment
        });
        
        saveDataToStorage();
        renderCategoryProfessionals();
        closeReviewModal();
        alert('Avaliação enviada com sucesso! Obrigado!');
    }
}

window.onclick = function(event) {
    const modal = document.getElementById('reviewModal');
    if (event.target === modal) {
        modal.style.display = 'none';
    }
}

// ============================================
// UPLOAD DE FOTO
// ============================================

function setupPhotoUpload() {
    const photoUploadArea = document.getElementById('photoUploadArea');
    const photoInput = document.getElementById('photo');
    const photoUploadButtons = document.getElementById('photoUploadButtons');
    
    if (!photoUploadArea) return;
    
    // Criar botões
    const cameraBtn = document.createElement('button');
    cameraBtn.type = 'button';
    cameraBtn.textContent = '📷 Tirar Foto';
    cameraBtn.style.cssText = `
        background: var(--primary-color);
        color: white;
        border: none;
        padding: 10px 20px;
        border-radius: 6px;
        cursor: pointer;
        font-weight: 600;
        transition: all 0.3s ease;
        flex: 1;
        min-width: 140px;
        margin-bottom: 10px;
    `;
    cameraBtn.onmouseover = () => cameraBtn.style.background = '#4f46e5';
    cameraBtn.onmouseout = () => cameraBtn.style.background = 'var(--primary-color)';
    cameraBtn.addEventListener('click', () => accessCamera());
    
    const galleryBtn = document.createElement('button');
    galleryBtn.type = 'button';
    galleryBtn.textContent = '🖼️ Galeria';
    galleryBtn.style.cssText = `
        background: var(--secondary-color);
        color: white;
        border: none;
        padding: 10px 20px;
        border-radius: 6px;
        cursor: pointer;
        font-weight: 600;
        transition: all 0.3s ease;
        flex: 1;
        min-width: 140px;
        margin-bottom: 10px;
    `;
    galleryBtn.onmouseover = () => galleryBtn.style.background = '#be185d';
    galleryBtn.onmouseout = () => galleryBtn.style.background = 'var(--secondary-color)';
    galleryBtn.addEventListener('click', () => photoInput.click());
    
    photoUploadButtons.style.cssText = `
        display: flex;
        gap: 10px;
        margin-bottom: 15px;
        flex-wrap: wrap;
    `;
    
    photoUploadButtons.appendChild(cameraBtn);
    photoUploadButtons.appendChild(galleryBtn);
    
    // Clique para galeria
    photoUploadArea.addEventListener('click', () => photoInput.click());
    
    // Drag and drop
    photoUploadArea.addEventListener('dragover', (e) => {
        e.preventDefault();
        photoUploadArea.style.borderColor = 'var(--primary-color)';
        photoUploadArea.style.background = 'rgba(99, 102, 241, 0.1)';
    });
    
    photoUploadArea.addEventListener('dragleave', () => {
        photoUploadArea.style.borderColor = 'var(--border-color)';
        photoUploadArea.style.background = 'var(--light-bg)';
    });
    
    photoUploadArea.addEventListener('drop', (e) => {
        e.preventDefault();
        photoUploadArea.style.borderColor = 'var(--border-color)';
        photoUploadArea.style.background = 'var(--light-bg)';
        
        const files = e.dataTransfer.files;
        if (files.length > 0) {
            photoInput.files = files;
            handlePhotoSelect();
        }
    });
    
    photoInput.addEventListener('change', handlePhotoSelect);
}

function accessCamera() {
    navigator.mediaDevices.getUserMedia({ 
        video: { facingMode: 'user' },
        audio: false 
    }).then(stream => {
        const video = document.createElement('video');
        video.srcObject = stream;
        video.setAttribute('autoplay', true);
        video.setAttribute('playsinline', true);
        video.style.cssText = `
            width: 100%;
            max-width: 400px;
            border-radius: 8px;
            margin: 10px 0;
        `;
        
        const cameraModal = document.createElement('div');
        cameraModal.style.cssText = `
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            padding: 20px;
        `;
        
        const content = document.createElement('div');
        content.style.cssText = `
            background: white;
            border-radius: 12px;
            padding: 20px;
            max-width: 500px;
            width: 100%;
        `;
        
        const title = document.createElement('h3');
        title.textContent = 'Tirar Foto';
        title.style.cssText = `
            margin-bottom: 15px;
            text-align: center;
            color: var(--text-dark);
        `;
        
        const canvas = document.createElement('canvas');
        
        const buttonsContainer = document.createElement('div');
        buttonsContainer.style.cssText = `
            display: flex;
            gap: 10px;
            margin-top: 15px;
        `;
        
        const captureBtn = document.createElement('button');
        captureBtn.textContent = '📸 Capturar';
        captureBtn.style.cssText = `
            flex: 1;
            background: var(--success-color);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 14px;
        `;
        
        captureBtn.addEventListener('click', () => {
            canvas.width = video.videoWidth;
            canvas.height = video.videoHeight;
            
            const ctx = canvas.getContext('2d');
            ctx.drawImage(video, 0, 0);
            
            photoDataUrl = canvas.toDataURL('image/jpeg', 0.9);
            
            const preview = document.getElementById('photoPreview');
            const previewImage = document.getElementById('previewImage');
            previewImage.src = photoDataUrl;
            preview.style.display = 'block';
            
            document.getElementById('photoError').textContent = '';
            
            stream.getTracks().forEach(track => track.stop());
            document.body.removeChild(cameraModal);
            
            alert('Foto capturada com sucesso! ✅');
        });
        
        const cancelBtn = document.createElement('button');
        cancelBtn.textContent = '❌ Cancelar';
        cancelBtn.style.cssText = `
            flex: 1;
            background: var(--error-color);
            color: white;
            border: none;
            padding: 12px;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            font-size: 14px;
        `;
        
        cancelBtn.addEventListener('click', () => {
            stream.getTracks().forEach(track => track.stop());
            document.body.removeChild(cameraModal);
        });
        
        buttonsContainer.appendChild(captureBtn);
        buttonsContainer.appendChild(cancelBtn);
        
        content.appendChild(title);
        content.appendChild(video);
        content.appendChild(buttonsContainer);
        cameraModal.appendChild(content);
        document.body.appendChild(cameraModal);
        
        setTimeout(() => {
            video.play();
        }, 100);
        
    }).catch(err => {
        console.error('Erro ao acessar câmera:', err);
        
        let mensagem = 'Erro ao acessar câmera';
        
        if (err.name === 'NotAllowedError') {
            mensagem = 'Permissão de câmera foi negada. Ative nas configurações do navegador.';
        } else if (err.name === 'NotFoundError') {
            mensagem = 'Câmera não encontrada no dispositivo.';
        }
        
        alert(mensagem);
    });
}

function handlePhotoSelect() {
    const photoInput = document.getElementById('photo');
    const file = photoInput.files[0];
    
    if (!file) return;
    
    if (file.size > 5 * 1024 * 1024) {
        alert('Arquivo muito grande! Máximo 5MB');
        photoInput.value = '';
        return;
    }
    
    if (!file.type.startsWith('image/')) {
        alert('Por favor, selecione uma imagem válida');
        photoInput.value = '';
        return;
    }
    
    const reader = new FileReader();
    reader.onload = (e) => {
        photoDataUrl = e.target.result;
        
        const preview = document.getElementById('photoPreview');
        const previewImage = document.getElementById('previewImage');
        
        previewImage.src = photoDataUrl;
        preview.style.display = 'block';
        
        document.getElementById('photoError').textContent = '';
    };
    
    reader.readAsDataURL(file);
}

// ============================================
// CADASTRO
// ============================================

function setupForm() {
    const form = document.getElementById('registrationForm');
    if (!form) return;
    
    form.addEventListener('submit', function(e) {
        e.preventDefault();
        
        const name = document.getElementById('name').value.trim();
        const category = document.getElementById('category').value;
        const description = document.getElementById('description').value.trim();
        const whatsapp = document.getElementById('whatsapp').value.trim();
        const city = document.getElementById('city').value.trim();
        
        let valid = true;
        
        if (name.length < 3) {
            document.getElementById('nameError').textContent = 'Nome deve ter no mínimo 3 caracteres';
            valid = false;
        } else {
            document.getElementById('nameError').textContent = '';
        }
        
        if (!category) {
            document.getElementById('categoryError').textContent = 'Selecione uma categoria';
            valid = false;
        } else {
            document.getElementById('categoryError').textContent = '';
        }
        
        const whatsappRegex = /^\(\d{2}\)\s9\d{4}-\d{4}$/;
        if (!whatsappRegex.test(whatsapp)) {
            document.getElementById('whatsappError').textContent = 'Formato: (XX) 9XXXX-XXXX';
            valid = false;
        } else {
            document.getElementById('whatsappError').textContent = '';
        }
        
        if (!city) {
            document.getElementById('cityError').textContent = 'Informe sua cidade';
            valid = false;
        } else {
            document.getElementById('cityError').textContent = '';
        }
        
        if (!photoDataUrl) {
            document.getElementById('photoError').textContent = 'Selecione uma foto';
            valid = false;
        } else {
            document.getElementById('photoError').textContent = '';
        }
        
        if (valid) {
            const newProfessional = {
                id: Math.max(...professionals.map(p => p.id), 0) + 1,
                name: name,
                category: category,
                description: description || 'Profissional qualificado',
                whatsapp: whatsapp,
                city: city,
                photo: photoDataUrl,
                reviews: []
            };
            
            professionals.push(newProfessional);
            saveDataToStorage();
            
            alert('Cadastro realizado com sucesso! 🎉');
            form.reset();
            photoDataUrl = null;
            document.getElementById('photoPreview').style.display = 'none';
            showHome();
            renderServices();
        }
    });
}  
