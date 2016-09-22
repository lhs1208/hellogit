SET FOREIGN_KEY_CHECKS = 0;

DROP DATABASE IF EXISTS `myschool`;
CREATE DATABASE `myschool`;
USE `myschool`;

-- ----------------------------
--  Table structure for `department`
-- ----------------------------
DROP TABLE IF EXISTS `department`;
CREATE TABLE `department` (
  `deptno` int(4) NOT NULL AUTO_INCREMENT COMMENT '부서번호(학과번호)',
  `dname` varchar(16) NOT NULL COMMENT '부서명(학과명)',
  `loc` varchar(10) DEFAULT NULL COMMENT '위치',
  PRIMARY KEY (`deptno`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='부서(학과) ';

-- ----------------------------
--  Records of `department`
-- ----------------------------
BEGIN;
INSERT INTO `department` VALUES ('101', '컴퓨터공학과', '1호관'), ('102', '멀티미디어학과', '2호관'), ('201', '전자공학과', '3호관'), ('202', '기계공학과', '4호관');
COMMIT;

-- ----------------------------
--  Table structure for `professor`
-- ----------------------------
DROP TABLE IF EXISTS `professor`;
CREATE TABLE `professor` (
  `profno` int(11) NOT NULL AUTO_INCREMENT COMMENT '교수번호',
  `name` varchar(10) NOT NULL COMMENT '이름 ',
  `userid` varchar(10) NOT NULL COMMENT '아이디',
  `position` varchar(20) NOT NULL COMMENT '직급 ',
  `sal` int(10) NOT NULL COMMENT '급여 ',
  `hiredate` datetime NOT NULL COMMENT '입사일',
  `comm` int(11) DEFAULT NULL COMMENT '보직수당',
  `deptno` int(11) NOT NULL COMMENT '부서번호(학과번호)',
  PRIMARY KEY (`profno`),
  KEY `deptno` (`deptno`),
  CONSTRAINT `fk_professor_department` FOREIGN KEY (`deptno`) REFERENCES `department` (`deptno`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='교수 테이블';

-- ----------------------------
--  Records of `professor`
-- ----------------------------
BEGIN;
INSERT INTO `professor` VALUES ('9901', '김도훈', 'capool', '교수', '500', '1982-06-12 00:00:00', '20', '101'), ('9902', '이재우', 'sweat413', '조교수', '320', '1995-04-12 00:00:00', null, '201'), ('9903', '성연희', 'pascal', '조교수', '360', '1993-03-17 00:00:00', '15', '101'), ('9904', '염일웅', 'blue77', '전임강사', '240', '1998-10-11 00:00:00', null, '102'), ('9905', '권혁일', 'refresh', '교수', '450', '1986-02-11 00:00:00', '25', '102'), ('9906', '이만식', 'pocari', '부교수', '420', '1988-07-11 00:00:00', null, '101'), ('9907', '전은지', 'totoro', '전임강사', '210', '2001-05-11 00:00:00', null, '101'), ('9908', '남은혁', 'bird13', '부교수', '400', '1990-10-18 00:00:00', '17', '202');
COMMIT;

-- ----------------------------
--  Table structure for `student`
-- ----------------------------
DROP TABLE IF EXISTS `student`;
CREATE TABLE `student` (
  `studno` int(11) NOT NULL AUTO_INCREMENT COMMENT '학생번호',
  `name` varchar(10) NOT NULL COMMENT '이름',
  `userid` varchar(10) NOT NULL COMMENT '아이디',
  `grade` int(11) NOT NULL COMMENT '학년',
  `idnum` varchar(13) NOT NULL COMMENT '주민번호',
  `birthdate` datetime NOT NULL COMMENT '생년월일',
  `tel` varchar(13) NOT NULL COMMENT '전화번호',
  `height` int(11) NOT NULL COMMENT '키',
  `weight` int(11) NOT NULL COMMENT '몸무게',
  `deptno` int(11) NOT NULL COMMENT '학과번호',
  `profno` int(11) DEFAULT NULL COMMENT '담당교수의 일련번호',
  PRIMARY KEY (`studno`),
  KEY `profno` (`profno`),
  KEY `deptno` (`deptno`),
  CONSTRAINT `fk_student_department` FOREIGN KEY (`deptno`) REFERENCES `department` (`deptno`),
  CONSTRAINT `fk_student_professor` FOREIGN KEY (`profno`) REFERENCES `professor` (`profno`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='학생테이블';

-- ----------------------------
--  Records of `student`
-- ----------------------------
BEGIN;
INSERT INTO `student` VALUES ('10101', '전인하', 'jun123', '4', '7907021369824', '1979-07-02 00:00:00', '051)781-2158', '176', '72', '101', '9903'), ('10102', '박미경', 'ansel414', '1', '8405162123648', '1984-05-16 00:00:00', '055)261-8947', '168', '52', '101', null), ('10103', '김영균', 'mandu', '3', '8103211063421', '1981-03-21 00:00:00', '051)824-9637', '170', '88', '101', '9906'), ('10104', '지은경', 'gomo00', '2', '8004122298371', '1980-04-12 00:00:00', '055)418-9627', '161', '42', '101', '9907'), ('10105', '임유진', 'youjin12', '2', '8301212196482', '1983-01-21 00:00:00', '02)312-9838', '171', '54', '101', '9907'), ('10106', '서재진', 'seolly', '1', '8511291186273', '1985-11-29 00:00:00', '051)239-4861', '186', '72', '101', null), ('10107', '이광훈', 'huriky', '4', '8109131276431', '1981-09-13 00:00:00', '055)736-4981', '175', '92', '101', '9903'), ('10108', '류민정', 'cleansky', '2', '8108192157498', '1981-08-19 00:00:00', '055)248-3679', '162', '72', '101', '9907'), ('10201', '김진영', 'simply', '2', '8206062186327', '1982-06-06 00:00:00', '055)419-6328', '164', '48', '102', '9905'), ('10202', '오유석', 'yousuk', '4', '7709121128379', '1977-09-12 00:00:00', '051)724-9618', '177', '92', '102', '9905'), ('10203', '하나리', 'hanal', '1', '8501092378641', '1985-01-09 00:00:00', '055)296-3784', '160', '68', '102', null), ('10204', '윤진욱', 'samba7', '3', '7904021358671', '1979-04-02 00:00:00', '053)487-2698', '171', '70', '102', '9905'), ('20101', '이동훈', 'dals', '1', '8312101128467', '1983-12-10 00:00:00', '055)426-1752', '172', '64', '201', null), ('20102', '박동진', 'ping2', '1', '8511241639826', '1985-11-24 00:00:00', '051)742-6384', '182', '70', '201', null), ('20103', '김진경', 'lovely', '2', '8302282169387', '1983-02-28 00:00:00', '052)175-3941', '166', '51', '201', '9902'), ('20104', '조명훈', 'rader214', '1', '8412141254963', '1984-12-14 00:00:00', '02)785-6984', '184', '62', '201', null);
COMMIT;

SET FOREIGN_KEY_CHECKS = 1;
