/* ==========================
   FILE: angular.json
   ========================== */
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "version": 1,
  "newProjectRoot": "projects",
  "projects": {
    "logic-app-monitor": {
      "projectType": "application",
      "schematics": {},
      "root": "",
      "sourceRoot": "src",
      "prefix": "app",
      "architect": {
        "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            "outputPath": "dist/logic-app-monitor",
            "index": "src/index.html",
            "main": "src/main.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "tsconfig.app.json",
            "assets": ["src/favicon.ico", "src/assets"],
            "styles": ["src/styles.css"],
            "scripts": []
          },
          "configurations": {
            "production": {
              "fileReplacements": [
                {
                  "replace": "src/environments/environment.ts",
                  "with": "src/environments/environment.prod.ts"
                }
              ],
              "optimization": true,
              "outputHashing": "all",
              "sourceMap": false,
              "extractCss": true,
              "namedChunks": false,
              "extractLicenses": true,
              "vendorChunk": false,
              "buildOptimizer": true
            }
          }
        },
        "serve": {
          "builder": "@angular-devkit/build-angular:dev-server",
          "options": {
            "browserTarget": "logic-app-monitor:build"
          },
          "configurations": {
            "production": {
              "browserTarget": "logic-app-monitor:build:production"
            }
          }
        }
      }
    }
  },
  "defaultProject": "logic-app-monitor"
}

/* ==========================
   FILE: src/app/app.module.ts
   ========================== */
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatToolbarModule } from '@angular/material/toolbar';
import { MatCardModule } from '@angular/material/card';
import { MatButtonModule } from '@angular/material/button';
import { MatIconModule } from '@angular/material/icon';
import { MatTableModule } from '@angular/material/table';
import { AppComponent } from './app.component';
import { DashboardComponent } from './components/dashboard/dashboard.component';
import { StatusCardComponent } from './components/status-card/status-card.component';
import { RouterModule, Routes } from '@angular/router';
import { NotificationSettingsComponent } from './components/notification-settings/notification-settings.component';
import { SelfHealComponent } from './components/self-heal/self-heal.component';

const routes: Routes = [
  { path: '', component: DashboardComponent },
  { path: 'notifications', component: NotificationSettingsComponent },
  { path: 'self-heal', component: SelfHealComponent }
];

@NgModule({
  declarations: [
    AppComponent,
    DashboardComponent,
    StatusCardComponent,
    NotificationSettingsComponent,
    SelfHealComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    RouterModule.forRoot(routes),
    MatToolbarModule,
    MatCardModule,
    MatButtonModule,
    MatIconModule,
    MatTableModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

/* ==========================
   FILE: src/app/app.component.html
   ========================== */
<mat-toolbar color="primary">
  Logic App Monitor
  <span class="spacer"></span>
  <button mat-button routerLink="/">Dashboard</button>
  <button mat-button routerLink="/notifications">Notifications</button>
  <button mat-button routerLink="/self-heal">Self-Heal</button>
</mat-toolbar>
<router-outlet></router-outlet>

/* ==========================
   FILE: src/app/components/dashboard/dashboard.component.ts
   ========================== */
import { Component } from '@angular/core';

@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
  styleUrls: ['./dashboard.component.css']
})
export class DashboardComponent {
  endpoints = [
    { name: 'Internal API', status: 'Green' },
    { name: 'External UI', status: 'Yellow' },
    { name: 'Auth Service', status: 'Red' }
  ];
}

/* ==========================
   FILE: src/app/components/dashboard/dashboard.component.html
   ========================== */
<div class="dashboard">
  <app-status-card *ngFor="let ep of endpoints" [endpoint]="ep"></app-status-card>
</div>

/* ==========================
   FILE: src/app/components/dashboard/dashboard.component.css
   ========================== */
.dashboard {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  flex-wrap: wrap;
}

/* ==========================
   FILE: src/app/components/status-card/status-card.component.ts
   ========================== */
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-status-card',
  templateUrl: './status-card.component.html',
  styleUrls: ['./status-card.component.css']
})
export class StatusCardComponent {
  @Input() endpoint: any;

  getStatusColor(status: string): string {
    switch (status) {
      case 'Green': return '#4caf50';
      case 'Yellow': return '#ffeb3b';
      case 'Red': return '#f44336';
      default: return '#ccc';
    }
  }
}

/* ==========================
   FILE: src/app/components/status-card/status-card.component.html
   ========================== */
<mat-card [style.border-left]="'5px solid ' + getStatusColor(endpoint.status)">
  <mat-card-title>{{ endpoint.name }}</mat-card-title>
  <mat-card-content>
    Status: <strong>{{ endpoint.status }}</strong>
  </mat-card-content>
</mat-card>

/* ==========================
   FILE: src/app/components/status-card/status-card.component.css
   ========================== */
mat-card {
  width: 200px;
}

/* ==========================
   FILE: src/app/components/notification-settings/notification-settings.component.ts
   ========================== */
import { Component } from '@angular/core';

@Component({
  selector: 'app-notification-settings',
  template: `<p>Notification settings will be here.</p>`
})
export class NotificationSettingsComponent {}

/* ==========================
   FILE: src/app/components/self-heal/self-heal.component.ts
   ========================== */
import { Component } from '@angular/core';

@Component({
  selector: 'app-self-heal',
  template: `<p>Self-heal automation configuration will be here.</p>`
})
export class SelfHealComponent {}

/* ==========================
   FILE: src/styles.css
   ========================== */
body {
  margin: 0;
  font-family: Roboto, sans-serif;
}

.spacer {
  flex: 1 1 auto;
}

mat-toolbar button {
  color: white;
}
