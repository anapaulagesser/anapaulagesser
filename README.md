cd chat-angular
git init
git remote add origin https://github.com/anapaulagesser/chat-angular.git
git add .
git commit -m "Primeiro commit do chat Angular"
git branch -M main
git push -u origin main

npx ng new chat-angular
cd chat-angular
ng serve
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  mensagemDigitada = '';
  mensagens: { texto: string, autor: 'atendente' | 'voce' }[] = [
    { texto: 'Blabla blabla blabla', autor: 'atendente' },
    { texto: 'Blabla blabla blabla', autor: 'atendente' },
    { texto: 'Blabla blabla blabla', autor: 'voce' },
    { texto: 'Blabla blabla blabla', autor: 'voce' }
  ];

  enviarMensagem() {
    if (this.mensagemDigitada.trim() !== '') {
      this.mensagens.push({ texto: this.mensagemDigitada, autor: 'voce' });
      this.mensagemDigitada = '';
    }
  }
}
<div class="chat-container">
  <h2>Atendimento on-line</h2>
  <div class="mensagens">
    <div *ngFor="let msg of mensagens" [ngClass]="msg.autor">
      <strong *ngIf="msg.autor === 'atendente'">Atendente diz:</strong>
      <strong *ngIf="msg.autor === 'voce'">Você diz:</strong>
      <div class="msg-box">{{ msg.texto }}</div>
    </div>
  </div>

  <div class="entrada">
    <input type="text" [(ngModel)]="mensagemDigitada" placeholder="Digite sua mensagem..." />
    <button (click)="enviarMensagem()">ENVIAR</button>
  </div>
</div>
.chat-container {
  width: 400px;
  margin: 0 auto;
  border: 2px solid #000;
  padding: 10px;
  font-family: sans-serif;
}

h2 {
  color: purple;
}

.mensagens {
  min-height: 200px;
  margin-bottom: 10px;
}

.atendente, .voce {
  margin: 10px 0;
}

.msg-box {
  border: 1px solid #888;
  padding: 5px 10px;
  margin-top: 2px;
  background-color: #f4f4f4;
  display: inline-block;
  max-width: 100%;
}

.entrada {
  display: flex;
}

input[type="text"] {
  flex: 1;
  padding: 5px;
}

button {
  padding: 5px 10px;
  margin-left: 5px;
  color: green;
  font-weight: bold;
}
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms'; // importe aqui

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule], // adicione aqui
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
