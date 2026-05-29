--作業一：班級適合外來鍵

-- 建立班級資料表
CREATE TABLE classes (
    id SERIAL PRIMARY KEY,     -- 班級編號，主鍵
    name VARCHAR(50)          -- 班級名稱
);

-- 建立學生資料表
CREATE TABLE students (
    id SERIAL PRIMARY KEY,   -- 學生編號，主鍵
    name VARCHAR(50),        -- 學生名稱
    class_id INTEGER,        -- 班級，外來鍵
    gender VARCHAR (2),      -- 性別
    age INTEGER,             -- 年齡
    FOREIGN KEY (class_id) REFERENCES classes(id)  -- 設定外來鍵關聯
);

-- 新增班級資料
INSERT INTO classes (name) VALUES 
    ('三年一班'),
    ('三年二班');

-- 新增學生資料
INSERT INTO students (name, class_id, gender, age) VALUES 
    ('小明', 1, '男', 8),
    ('小華', 2, '女', 9),
    ('小美', 1, '男', 8),
    ('小強', 1, '女', 8),
    ('小智', 2, '男', 9);
    
SELECT 
    students.name AS 學生姓名,
    students.gender AS 性別,
    students.age AS 年齡,
    classes.name AS 班級姓名
FROM students
INNER JOIN classes ON students.class_id = classes.id


--作業二：

-- 建立教師資料表
CREATE TABLE teachers (
    id SERIAL PRIMARY KEY,     -- 教師編號，主鍵
    name VARCHAR(50),          -- 教師名稱
);

-- 建立班級資料表
CREATE TABLE classes(
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    teacher_id INTEGER,
    FOREIGN KEY(teacher_id) REFERENCES teachers(id)
);

-- 建立學生資料表
CREATE TABLE students(
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    class_id INTEGER,
    gender VARCHAR(2),
    age INTEGER,
    FOREIGN KEY(class_id) REFERENCES classes(id)
)

-- 新增教師資料
INSERT INTO teachers (name) VALUES 
    ('廖洧杰'), ('卡斯伯');

-- 新增班級資料
INSERT INTO classes (name, teacher_id) VALUES
    ('三年一班',1),
    ('三年二班',2);

-- 新增學生資料
INSERT INTO students (name, class_id, gender, age) VALUES
    ('小明', 1, '男', 8),
    ('小華', 2, '女', 9),
    ('小美', 1, '男', 8),
    ('小強', 1, '女', 8),
    ('小智', 2, '男', 9);
    
SELECT 
    s.name AS 學生姓名,
    c.name AS 班級,
    t.name AS 班級老師,
    s.gender AS 性別,
    s.age AS 年齡
FROM students s
INNER JOIN classes c ON s.class_id = c.id
INNER JOIN teachers t ON c.teacher_id = t.id;

--作業三：

-- 建立父母資料表
CREATE TABLE parents (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    phone VARCHAR(20),
    gender VARCHAR(2)
);

-- 建立小孩資料表
CREATE TABLE children(
    id SERIAL PRIMARY KEY,
    name VARCHAR(50),
    parent_id INTEGER,
    FOREIGN KEY(parent_id) REFERENCE parents(id)
);

-- 新增父母資料
INSERT INTO parents (name, phone, gender) VALUES
    ('王大祥', '0973254254', '男'),
    ('王曉茹', '0955717855', '女');
    
-- 新增小孩資料
INSERT INTO parents (name, parent_id) VALUES
    ('小明',1),
    ('小華',2),
    ('小美',1),
    ('小強',2),
    ('小智',1);
    
SELECT 
    children.id AS 小孩編號,
    children.name AS 姓名,
    parents.name AS 父母名稱,
    parents.phone AS 父母電話,
    parents.gender AS 父母性別
FROM children
INNER JOIN parents ON children.parent_id = parents.id