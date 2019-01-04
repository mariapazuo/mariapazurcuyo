-- MySQL Workbench Forward Engineering

SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0;
SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0;
SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION';

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------

-- -----------------------------------------------------
-- Schema mydb
-- -----------------------------------------------------
CREATE SCHEMA IF NOT EXISTS `mydb` DEFAULT CHARACTER SET utf8 ;
USE `mydb` ;

-- -----------------------------------------------------
-- Table `mydb`.`dirección`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`dirección` (
  `iddirección` INT NOT NULL,
  PRIMARY KEY (`iddirección`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`sexo`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`sexo` (
  `idsexo` INT NOT NULL,
  `nombre` VARCHAR(1) NULL,
  PRIMARY KEY (`idsexo`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`username`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`username` (
  `idusername` INT NOT NULL,
  `correo` VARCHAR(50) NOT NULL,
  `contraseña` VARCHAR(20) NOT NULL,
  `fecha de nacimiento` DATE NOT NULL,
  `correo` VARCHAR(45) NOT NULL,
  `dirección_iddirección` INT NOT NULL,
  `sexo_idsexo` INT NOT NULL,
  PRIMARY KEY (`idusername`),
  INDEX `fk_username_dirección1_idx` (`dirección_iddirección` ASC) VISIBLE,
  INDEX `fk_username_sexo1_idx` (`sexo_idsexo` ASC) VISIBLE,
  CONSTRAINT `fk_username_dirección1`
    FOREIGN KEY (`dirección_iddirección`)
    REFERENCES `mydb`.`dirección` (`iddirección`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_username_sexo1`
    FOREIGN KEY (`sexo_idsexo`)
    REFERENCES `mydb`.`sexo` (`idsexo`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`avance`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`avance` (
  `idavance` INT NOT NULL,
  `lección aprobada` INT NOT NULL,
  `nivel de dificultad` VARCHAR(30) NOT NULL,
  PRIMARY KEY (`idavance`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`teoría`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`teoría` (
  `idteoría` INT NOT NULL,
  PRIMARY KEY (`idteoría`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`lecciones`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`lecciones` (
  `idlecciones` INT NOT NULL,
  `teoría_idteoría` INT NOT NULL,
  PRIMARY KEY (`idlecciones`),
  INDEX `fk_lecciones_teoría1_idx` (`teoría_idteoría` ASC) VISIBLE,
  CONSTRAINT `fk_lecciones_teoría1`
    FOREIGN KEY (`teoría_idteoría`)
    REFERENCES `mydb`.`teoría` (`idteoría`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`práctica`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`práctica` (
  `idpráctica` INT NOT NULL,
  `lecciones_idlecciones` INT NOT NULL,
  PRIMARY KEY (`idpráctica`),
  INDEX `fk_práctica_lecciones1_idx` (`lecciones_idlecciones` ASC) VISIBLE,
  CONSTRAINT `fk_práctica_lecciones1`
    FOREIGN KEY (`lecciones_idlecciones`)
    REFERENCES `mydb`.`lecciones` (`idlecciones`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`dificultad`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`dificultad` (
  `iddificultad` INT NOT NULL,
  PRIMARY KEY (`iddificultad`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`tipo`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`tipo` (
  `idtipo` INT NOT NULL,
  PRIMARY KEY (`idtipo`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`preguntas`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`preguntas` (
  `idpreguntas` INT NOT NULL,
  `práctica_idpráctica` INT NOT NULL,
  `dificultad_iddificultad` INT NOT NULL,
  `tipo_idtipo` INT NOT NULL,
  PRIMARY KEY (`idpreguntas`),
  INDEX `fk_preguntas_práctica1_idx` (`práctica_idpráctica` ASC) VISIBLE,
  INDEX `fk_preguntas_dificultad1_idx` (`dificultad_iddificultad` ASC) VISIBLE,
  INDEX `fk_preguntas_tipo1_idx` (`tipo_idtipo` ASC) VISIBLE,
  CONSTRAINT `fk_preguntas_práctica1`
    FOREIGN KEY (`práctica_idpráctica`)
    REFERENCES `mydb`.`práctica` (`idpráctica`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_preguntas_dificultad1`
    FOREIGN KEY (`dificultad_iddificultad`)
    REFERENCES `mydb`.`dificultad` (`iddificultad`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_preguntas_tipo1`
    FOREIGN KEY (`tipo_idtipo`)
    REFERENCES `mydb`.`tipo` (`idtipo`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`comunidad sorda`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`comunidad sorda` (
  `idblog` INT NOT NULL,
  `texto` VARCHAR(300) NOT NULL,
  `likes` INT NOT NULL,
  `comentarios` INT NOT NULL,
  `imagen` BLOB NOT NULL,
  `comunidad sorda_idcomunidad sorda` INT NOT NULL,
  PRIMARY KEY (`idblog`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`blogxusername`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`blogxusername` (
  `blog_idblog` INT NOT NULL,
  `username_idusername` INT NOT NULL,
  `idBlogxusername` INT NOT NULL,
  INDEX `fk_blog_has_username_username1_idx` (`username_idusername` ASC) VISIBLE,
  INDEX `fk_blog_has_username_blog1_idx` (`blog_idblog` ASC) VISIBLE,
  PRIMARY KEY (`idBlogxusername`),
  CONSTRAINT `fk_blog_has_username_blog1`
    FOREIGN KEY (`blog_idblog`)
    REFERENCES `mydb`.`comunidad sorda` (`idblog`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_blog_has_username_username1`
    FOREIGN KEY (`username_idusername`)
    REFERENCES `mydb`.`username` (`idusername`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`comentarios`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`comentarios` (
  `idcomentarios` INT NOT NULL,
  `texto` VARCHAR(150) NOT NULL,
  `blog_idblog` INT NOT NULL,
  `usernamexcomentario_úsernamexcomentariocol` INT NOT NULL,
  `username_idusername` INT NOT NULL,
  PRIMARY KEY (`idcomentarios`),
  INDEX `fk_comentarios_blog1_idx` (`blog_idblog` ASC) VISIBLE,
  INDEX `fk_comentarios_username1_idx` (`username_idusername` ASC) VISIBLE,
  CONSTRAINT `fk_comentarios_blog1`
    FOREIGN KEY (`blog_idblog`)
    REFERENCES `mydb`.`comunidad sorda` (`idblog`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_comentarios_username1`
    FOREIGN KEY (`username_idusername`)
    REFERENCES `mydb`.`username` (`idusername`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`eventos`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`eventos` (
  `ideventos` INT NOT NULL,
  `nombre` VARCHAR(30) NOT NULL,
  `descripcion` VARCHAR(100) NOT NULL,
  `fecha` DATE NOT NULL,
  `lugar` VARCHAR(45) NOT NULL,
  `comunidad sorda_idblog` INT NOT NULL,
  PRIMARY KEY (`ideventos`),
  INDEX `fk_eventos_comunidad sorda1_idx` (`comunidad sorda_idblog` ASC) VISIBLE,
  CONSTRAINT `fk_eventos_comunidad sorda1`
    FOREIGN KEY (`comunidad sorda_idblog`)
    REFERENCES `mydb`.`comunidad sorda` (`idblog`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`usernamexlecciones`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`usernamexlecciones` (
  `username_idusername` INT NOT NULL,
  `lecciones_idlecciones` INT NOT NULL,
  `idUsernamexlecciones` INT NOT NULL,
  `avance_idavance` INT NOT NULL,
  INDEX `fk_username_has_lecciones_lecciones1_idx` (`lecciones_idlecciones` ASC) VISIBLE,
  INDEX `fk_username_has_lecciones_username1_idx` (`username_idusername` ASC) VISIBLE,
  PRIMARY KEY (`idUsernamexlecciones`),
  INDEX `fk_usernamexlecciones_avance1_idx` (`avance_idavance` ASC) VISIBLE,
  CONSTRAINT `fk_username_has_lecciones_username1`
    FOREIGN KEY (`username_idusername`)
    REFERENCES `mydb`.`username` (`idusername`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_username_has_lecciones_lecciones1`
    FOREIGN KEY (`lecciones_idlecciones`)
    REFERENCES `mydb`.`lecciones` (`idlecciones`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_usernamexlecciones_avance1`
    FOREIGN KEY (`avance_idavance`)
    REFERENCES `mydb`.`avance` (`idavance`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`país`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`país` (
  `idpais` INT NOT NULL,
  `nombre` VARCHAR(45) NOT NULL,
  PRIMARY KEY (`idpais`))
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`provincias`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`provincias` (
  `idprovincias` INT NOT NULL,
  `nombre` VARCHAR(45) NOT NULL,
  `país_idpais` INT NOT NULL,
  PRIMARY KEY (`idprovincias`),
  INDEX `fk_provincias_país1_idx` (`país_idpais` ASC) VISIBLE,
  CONSTRAINT `fk_provincias_país1`
    FOREIGN KEY (`país_idpais`)
    REFERENCES `mydb`.`país` (`idpais`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`cantón`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`cantón` (
  `idcantón` INT NOT NULL,
  `nombre` VARCHAR(20) NULL,
  `provincias_idprovincias` INT NOT NULL,
  PRIMARY KEY (`idcantón`),
  INDEX `fk_cantón_provincias1_idx` (`provincias_idprovincias` ASC) VISIBLE,
  CONSTRAINT `fk_cantón_provincias1`
    FOREIGN KEY (`provincias_idprovincias`)
    REFERENCES `mydb`.`provincias` (`idprovincias`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


-- -----------------------------------------------------
-- Table `mydb`.`distrito`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `mydb`.`distrito` (
  `iddistrito` INT NOT NULL,
  `nombre` VARCHAR(45) NOT NULL,
  `cantón_idcantón` INT NOT NULL,
  `dirección_iddirección` INT NOT NULL,
  PRIMARY KEY (`iddistrito`),
  INDEX `fk_distrito_cantón1_idx` (`cantón_idcantón` ASC) VISIBLE,
  INDEX `fk_distrito_dirección1_idx` (`dirección_iddirección` ASC) VISIBLE,
  CONSTRAINT `fk_distrito_cantón1`
    FOREIGN KEY (`cantón_idcantón`)
    REFERENCES `mydb`.`cantón` (`idcantón`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION,
  CONSTRAINT `fk_distrito_dirección1`
    FOREIGN KEY (`dirección_iddirección`)
    REFERENCES `mydb`.`dirección` (`iddirección`)
    ON DELETE NO ACTION
    ON UPDATE NO ACTION)
ENGINE = InnoDB;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;
