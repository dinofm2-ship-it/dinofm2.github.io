<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SkillBoost - База данных курсов повышения квалификации</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --accent: #4cc9f0;
            --light: #f8f9fa;
            --dark: #212529;
            --success: #4bb543;
            --warning: #ffcc00;
            --danger: #dc3545;
        }
        
        body {
            background-color: #f5f7fa;
            color: var(--dark);
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 25px 0;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            margin-bottom: 30px;
            border-radius: 0 0 10px 10px;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo i {
            font-size: 2.5rem;
            color: var(--accent);
        }
        
        .logo-text h1 {
            font-size: 2.2rem;
            margin-bottom: 5px;
        }
        
        .logo-text p {
            opacity: 0.9;
            font-size: 1rem;
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 10px;
            background: rgba(255, 255, 255, 0.2);
            padding: 10px 15px;
            border-radius: 50px;
        }
        
        .user-info i {
            font-size: 1.5rem;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .stat-card {
            background: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            display: flex;
            align-items: center;
            gap: 20px;
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .stat-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
        }
        
        .stat-icon {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
        }
        
        .stat-icon.groups {
            background: rgba(67, 97, 238, 0.15);
            color: var(--primary);
        }
        
        .stat-icon.teachers {
            background: rgba(76, 201, 240, 0.15);
            color: var(--accent);
        }
        
        .stat-icon.disciplines {
            background: rgba(58, 12, 163, 0.15);
            color: var(--secondary);
        }
        
        .stat-icon.hours {
            background: rgba(75, 181, 67, 0.15);
            color: var(--success);
        }
        
        .stat-info h3 {
            font-size: 1rem;
            color: #6c757d;
            margin-bottom: 5px;
        }
        
        .stat-value {
            font-size: 2rem;
            font-weight: 700;
            color: var(--dark);
        }
        
        .tabs {
            display: flex;
            background-color: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            margin-bottom: 25px;
        }
        
        .tab {
            flex: 1;
            padding: 18px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 600;
            color: #555;
            border-bottom: 3px solid transparent;
        }
        
        .tab:hover {
            background-color: #f8f9fa;
            color: var(--primary);
        }
        
        .tab.active {
            background-color: white;
            color: var(--primary);
            border-bottom: 3px solid var(--primary);
        }
        
        .content {
            display: none;
            background-color: white;
            border-radius: 10px;
            padding: 25px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
            margin-bottom: 30px;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .content.active {
            display: block;
        }
        
        .content-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }
        
        .content-header h2 {
            color: var(--primary);
            font-size: 1.8rem;
        }
        
        .actions {
            display: flex;
            gap: 15px;
        }
        
        .btn {
            padding: 10px 20px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }
        
        .btn-primary {
            background-color: var(--primary);
            color: white;
        }
        
        .btn-primary:hover {
            background-color: var(--secondary);
        }
        
        .btn-outline {
            background-color: transparent;
            border: 1px solid var(--primary);
            color: var(--primary);
        }
        
        .btn-outline:hover {
            background-color: rgba(67, 97, 238, 0.1);
        }
        
        .search-box {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .search-input {
            flex: 1;
            padding: 12px 15px;
            border: 1px solid #ddd;
            border-radius: 6px;
            font-size: 1rem;
            transition: border 0.3s;
        }
        
        .search-input:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        
        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #e9ecef;
        }
        
        th {
            background-color: #f8f9fa;
            font-weight: 600;
            color: var(--dark);
            position: sticky;
            top: 0;
        }
        
        tr:hover {
            background-color: #f8f9fa;
        }
        
        .badge {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 600;
        }
        
        .badge-primary {
            background-color: rgba(67, 97, 238, 0.15);
            color: var(--primary);
        }
        
        .badge-success {
            background-color: rgba(75, 181, 67, 0.15);
            color: var(--success);
        }
        
        .badge-warning {
            background-color: rgba(255, 204, 0, 0.15);
            color: #b38f00;
        }
        
        footer {
            text-align: center;
            margin-top: 40px;
            padding: 25px;
            color: #6c757d;
            border-top: 1px solid #e9ecef;
        }
        
        @media (max-width: 768px) {
            .header-content {
                flex-direction: column;
                gap: 20px;
                text-align: center;
            }
            
            .tabs {
                flex-direction: column;
            }
            
            .content-header {
                flex-direction: column;
                gap: 15px;
                align-items: flex-start;
            }
            
            .actions {
                width: 100%;
                justify-content: space-between;
            }
            
            th, td {
                padding: 10px 8px;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="header-content">
                <div class="logo">
                    <i class="fas fa-graduation-cap"></i>
                    <div class="logo-text">
                        <h1>SkillBoost</h1>
                        <p>База данных курсов повышения квалификации</p>
                    </div>
                </div>
                <div class="user-info">
                    <i class="fas fa-user-circle"></i>
                    <span>Администратор</span>
                </div>
            </div>
        </div>
    </header>
    
    <div class="container">
        <div class="stats">
            <div class="stat-card">
                <div class="stat-icon groups">
                    <i class="fas fa-users"></i>
                </div>
                <div class="stat-info">
                    <h3>Всего групп</h3>
                    <div class="stat-value">12</div>
                </div>
            </div>
            <div class="stat-card">
                <div class="stat-icon teachers">
                    <i class="fas fa-chalkboard-teacher"></i>
                </div>
                <div class="stat-info">
                    <h3>Преподавателей</h3>
                    <div class="stat-value">25</div>
                </div>
            </div>
            <div class="stat-card">
                <div class="stat-icon disciplines">
                    <i class="fas fa-book"></i>
                </div>
                <div class="stat-info">
                    <h3>Дисциплин</h3>
                    <div class="stat-value">18</div>
                </div>
            </div>
            <div class="stat-card">
                <div class="stat-icon hours">
                    <i class="fas fa-clock"></i>
                </div>
                <div class="stat-info">
                    <h3>Общее количество часов</h3>
                    <div class="stat-value">1,240</div>
                </div>
            </div>
        </div>
        
        <div class="tabs">
            <div class="tab active" data-tab="groups">
                <i class="fas fa-users"></i> Группы
            </div>
            <div class="tab" data-tab="teachers">
                <i class="fas fa-chalkboard-teacher"></i> Преподаватели
            </div>
            <div class="tab" data-tab="workload">
                <i class="fas fa-tasks"></i> Учебная нагрузка
            </div>
        </div>
        
        <div class="content active" id="groups-content">
            <div class="content-header">
                <h2>Список групп</h2>
                <div class="actions">
                    <button class="btn btn-outline">
                        <i class="fas fa-file-export"></i> Экспорт
                    </button>
                    <button class="btn btn-primary">
                        <i class="fas fa-plus"></i> Добавить группу
                    </button>
                </div>
            </div>
            <div class="search-box">
                <input type="text" class="search-input" placeholder="Поиск по номеру группы или программе...">
                <button class="btn btn-primary">
                    <i class="fas fa-search"></i> Найти
                </button>
            </div>
            <table>
                <thead>
                    <tr>
                        <th>Код группы</th>
                        <th>Номер группы</th>
                        <th>Наименование программы</th>
                        <th>Форма обучения</th>
                        <th>Количество обучающихся</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>GR001</td>
                        <td>ПК-101</td>
                        <td>Программирование на Python</td>
                        <td><span class="badge badge-primary">Очная</span></td>
                        <td>25</td>
                    </tr>
                    <tr>
                        <td>GR002</td>
                        <td>ПК-102</td>
                        <td>Веб-разработка</td>
                        <td><span class="badge badge-warning">Очно-заочная</span></td>
                        <td>30</td>
                    </tr>
                    <tr>
                        <td>GR003</td>
                        <td>ПК-103</td>
                        <td>Базы данных и SQL</td>
                        <td><span class="badge badge-primary">Очная</span></td>
                        <td>20</td>
                    </tr>
                    <tr>
                        <td>GR004</td>
                        <td>ПК-104</td>
                        <td>Кибербезопасность</td>
                        <td><span class="badge badge-success">Заочная</span></td>
                        <td>35</td>
                    </tr>
                    <tr>
                        <td>GR005</td>
                        <td>ПК-105</td>
                        <td>Машинное обучение</td>
                        <td><span class="badge badge-primary">Очная</span></td>
                        <td>18</td>
                    </tr>
                </tbody>
            </table>
        </div>
        
        <div class="content" id="teachers-content">
            <div class="content-header">
                <h2>Список преподавателей</h2>
                <div class="actions">
                    <button class="btn btn-outline">
                        <i class="fas fa-file-export"></i> Экспорт
                    </button>
                    <button class="btn btn-primary">
                        <i class="fas fa-plus"></i> Добавить преподавателя
                    </button>
                </div>
            </div>
            <div class="search-box">
                <input type="text" class="search-input" placeholder="Поиск по фамилии...">
                <button class="btn btn-primary">
                    <i class="fas fa-search"></i> Найти
                </button>
            </div>
            <table>
                <thead>
                    <tr>
                        <th>Код преподавателя</th>
                        <th>Фамилия</th>
                        <th>Имя</th>
                        <th>Отчество</th>
                        <th>Номер телефона</th>
                        <th>Стаж (лет)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>T001</td>
                        <td>Иванов</td>
                        <td>Алексей</td>
                        <td>Петрович</td>
                        <td>+7 (912) 345-67-89</td>
                        <td>15</td>
                    </tr>
                    <tr>
                        <td>T002</td>
                        <td>Петрова</td>
                        <td>Мария</td>
                        <td>Сергеевна</td>
                        <td>+7 (923) 456-78-90</td>
                        <td>10</td>
                    </tr>
                    <tr>
                        <td>T003</td>
                        <td>Сидоров</td>
                        <td>Дмитрий</td>
                        <td>Владимирович</td>
                        <td>+7 (934) 567-89-01</td>
                        <td>8</td>
                    </tr>
                    <tr>
                        <td>T004</td>
                        <td>Кузнецова</td>
                        <td>Ольга</td>
                        <td>Александровна</td>
                        <td>+7 (945) 678-90-12</td>
                        <td>12</td>
                    </tr>
                    <tr>
                        <td>T005</td>
                        <td>Васильев</td>
                        <td>Сергей</td>
                        <td>Игоревич</td>
                        <td>+7 (956) 789-01-23</td>
                        <td>7</td>
                    </tr>
                </tbody>
            </table>
        </div>
        
        <div class="content" id="workload-content">
            <div class="content-header">
                <h2>Учебная нагрузка преподавателей</h2>
                <div class="actions">
                    <button class="btn btn-outline">
                        <i class="fas fa-file-export"></i> Экспорт
                    </button>
                    <button class="btn btn-primary">
                        <i class="fas fa-plus"></i> Назначить нагрузку
                    </button>
                </div>
            </div>
            <div class="search-box">
                <input type="text" class="search-input" placeholder="Поиск по дисциплине или виду занятия...">
                <button class="btn btn-primary">
                    <i class="fas fa-search"></i> Найти
                </button>
            </div>
            <table>
                <thead>
                    <tr>
                        <th>Код преподавателя</th>
                        <th>Номер группы</th>
                        <th>Дисциплина</th>
                        <th>Количество часов</th>
                        <th>Вид занятия</th>
                        <th>Оплата (руб/час)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>T001</td>
                        <td>ПК-101</td>
                        <td>Программирование на Python</td>
                        <td>40</td>
                        <td><span class="badge badge-primary">Лекция</span></td>
                        <td>800</td>
                    </tr>
                    <tr>
                        <td>T001</td>
                        <td>ПК-101</td>
                        <td>Программирование на Python</td>
                        <td>30</td>
                        <td><span class="badge badge-warning">Практическое занятие</span></td>
                        <td>600</td>
                    </tr>
                    <tr>
                        <td>T002</td>
                        <td>ПК-102</td>
                        <td>Веб-разработка</td>
                        <td>35</td>
                        <td><span class="badge badge-primary">Лекция</span></td>
                        <td>750</td>
                    </tr>
                    <tr>
                        <td>T002</td>
                        <td>ПК-102</td>
                        <td>Веб-разработка</td>
                        <td>25</td>
                        <td><span class="badge badge-success">Лабораторная работа</span></td>
                        <td>700</td>
                    </tr>
                    <tr>
                        <td>T003</td>
                        <td>ПК-103</td>
                        <td>Базы данных и SQL</td>
                        <td>30</td>
                        <td><span class="badge badge-primary">Лекция</span></td>
                        <td>800</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    
    <footer>
        <div class="container">
            <p>© 2023 SkillBoost. База данных "Курсы повышения квалификации"</p>
            <p>Образовательное учреждение</p>
        </div>
    </footer>
    
    <script>
        // Табы переключения между разделами
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', () => {
                // Убираем активный класс у всех табов
                document.querySelectorAll('.tab').forEach(t => {
                    t.classList.remove('active');
                });
                
                // Добавляем активный класс текущему табу
                tab.classList.add('active');
                
                // Скрываем все контенты
                document.querySelectorAll('.content').forEach(content => {
                    content.classList.remove('active');
                });
                
                // Показываем соответствующий контент
                const tabId = tab.getAttribute('data-tab');
                document.getElementById(`${tabId}-content`).classList.add('active');
            });
        });
        
        // Простая функция поиска (для демонстрации)
        document.querySelectorAll('.btn-primary').forEach(button => {
            if (button.textContent.includes('Найти')) {
                button.addEventListener('click', () => {
                    const searchInput = button.parentElement.querySelector('.search-input');
                    if (searchInput.value.trim() === '') {
                        alert('Введите поисковый запрос');
                    } else {
                        alert(`Поиск: "${searchInput.value}"\nФункция поиска находится в разработке`);
                    }
                });
            }
        });
        
        // Обработка кнопок добавления
        document.querySelectorAll('.btn-primary').forEach(button => {
            if (button.textContent.includes('Добавить') || button.textContent.includes('Назначить')) {
                button.addEventListener('click', () => {
                    alert('Форма добавления новой записи будет открыта здесь');
                });
            }
        });
    </script>
</body>
</html>
