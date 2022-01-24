#  Curso de Python 3 do Básico ao Avançado 
#### Desafio: Criar um redimensionador de imagem

#### Para criar o layout do programa foi utilizado o Qt Designer

![imagem do Qt Designer](https://github.com/diegoguedes91/redimensionador_de_imagem/blob/main/imagens/QT_Designer.png)

Após salvar o arquivo deve converter o arquivo gerado em .ui para .py. </br>
No linux utilizei o comando _pyuic5 design.ui -o design.py_ no terminal. </br>
É feito esta conversão de arquivos pois necessita importar a classe _Ui_MainWindow_ gerado pelo Qt Designer.

```python
import sys
from design import *
from PyQt5.QtWidgets import QMainWindow, QApplication, QFileDialog
from PyQt5.QtGui import QPixmap

class RedimensionarImagem(QMainWindow, Ui_MainWindow):
    def __init__(self, parent=None):
        super().__init__(parent)
        super().setupUi(self)
        self.btnEscolherArquivo.clicked.connect(self.abrir_imagem)
        self.btnRedimensionar.clicked.connect(self.redimensionar)
        self.btnSalvar.clicked.connect(self.salvar)
 ```
 
### Abaixo estão definidas as funções: 

#### 1. Abrir a imagem:

```python
    def abrir_imagem(self):
        imagem, _ = QFileDialog.getOpenFileName(
            self.centralwidget,
            'abrir imagem',
            r'/home/diego/Pictures',
            options=QFileDialog.DontUseNativeDialog
        )
        self.inputAbrirArquivo.setText(imagem)
        self.original_img = QPixmap(imagem)
        self.labelImg.setPixmap(self.original_img)
        self.inputLargura.setText(str(self.original_img.width()))
        self.inputAltura.setText(str(self.original_img.height()))
  ```
  Ao clicar no botão _Escolher Imagem_ é aberto uma janela para o usuário escolher uma imagem. </br>
  Obs: o programa esta configurado para abrir na minha maquina ou seja no _/home/diego/Pictures_, basta trocar o local caso queira utilizar este codigo. </br>
  
  ![Abrindo imagem](https://github.com/diegoguedes91/redimensionador_de_imagem/blob/main/imagens/selecionar_imagem.png)
  
  Após escolher a imagem ela abrira no programa conforme as suas dimensões. 
  
  ![Abrindo imagem](https://github.com/diegoguedes91/redimensionador_de_imagem/blob/main/imagens/imagem_aberta.png)
  
  #### 2. Redimensionar a imagem:
```python
    def redimensionar(self):
        largura = int(self.inputLargura.text())
        self.nova_imagem = self.original_img.scaledToWidth(largura)
        self.labelImg.setPixmap(self.nova_imagem)
        self.inputLargura.setText(str(self.nova_imagem.width()))
        self.inputAltura.setText(str(self.nova_imagem.height()))
  ```
  O usuário deve inserir a largura ou altura que a imagem deve ter e clicar no botão _Redimensionar_.
  
   ![Redimensionar imagem](https://github.com/diegoguedes91/redimensionador_de_imagem/blob/main/imagens/imagem_redimensionada.png)
   
   #### 3. Salvando a imagem:
```python
       def salvar(self):
        imagem, _ = QFileDialog.getSaveFileName(
            self.centralwidget,
            'Salvar imagem',
            r'/home/diego/Desktop',
            options=QFileDialog.DontUseNativeDialog
        )
        self.nova_imagem.save(imagem, 'PNG')
```
    
   Finalmente, quando a imagem estiver nas dimensões desejadas basta clicar em no botão salvar. </br>
   Obs: O programa abre direto _/home/diego/Desktop_, basta fazer a alteração do caminho para utilizar o codigo. 
   
   ![Salvando imagem](https://github.com/diegoguedes91/redimensionador_de_imagem/blob/main/imagens/salvando_imagem.png)

### Para executar e abrir a aplicação: 
```python
if __name__ == '__main__':
    qt = QApplication(sys.argv)
    novo = RedimensionarImagem()
    novo.show()
    qt.exec()
 ```
  
