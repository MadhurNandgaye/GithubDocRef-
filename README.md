/* Angular project structure for Logic App Monitor UI */

// File: angular.json
// [Basic Angular config with Material theming enabled]

// File: src/index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>LogicAppMonitor</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>
  <app-root></app-root>
</body>
</html>

// File: src/main.ts
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));

// File: src/app/app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { HttpClientModule } from '@angular/common/http';
import { MatToolbarModule } from '@angular/material/toolbar';
import { MatCardModule } from '@angular/material/card';
import { MatButtonModule } from '@angular/material/button';
import { MatIconModule } from '@angular/material/icon';
import { MatTableModule } from '@angular/material/table';
import { MatSnackBarModule } from '@angular/material/snack-bar';
import { MatProgressSpinnerModule } from '@angular/material/progress-spinner';
import { AppComponent } from './app.component';
import { DashboardComponent } from './components/dashboard/dashboard.component';
import { StatusCardComponent } from './components/status-card/status-card.component';
import { NotificationSettingsComponent } from './components/notification-settings/notification-settings.component';
import { SelfHealComponent } from './components/self-heal/self-heal.component';
import { AppRoutingModule } from './app-routing.module';

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
    HttpClientModule,
    AppRoutingModule,
    MatToolbarModule,
    MatCardModule,
    MatButtonModule,
    MatIconModule,
    MatTableModule,
    MatSnackBarModule,
    MatProgressSpinnerModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

// File: src/app/app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { DashboardComponent } from './components/dashboard/dashboard.component';
import { NotificationSettingsComponent } from './components/notification-settings/notification-settings.component';
import { SelfHealComponent } from './components/self-heal/self-heal.component';

const routes: Routes = [
  { path: '', component: DashboardComponent },
  { path: 'notifications', component: NotificationSettingsComponent },
  { path: 'self-heal', component: SelfHealComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

// File: src/app/app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <mat-toolbar color="primary">Logic App Monitor</mat-toolbar>
    <router-outlet></router-outlet>
  `
})
export class AppComponent { }

// File: src/app/components/dashboard/dashboard.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html'
})
export class DashboardComponent { }

// File: src/app/components/dashboard/dashboard.component.html
<div class="dashboard">
  <app-status-card [endpoint]="'Internal Network'" [status]="'Green'"></app-status-card>
  <app-status-card [endpoint]="'Public Internet'" [status]="'Yellow'"></app-status-card>
</div>

// File: src/app/components/status-card/status-card.component.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-status-card',
  templateUrl: './status-card.component.html',
  styleUrls: ['./status-card.component.css']
})
export class StatusCardComponent {
  @Input() endpoint: string = '';
  @Input() status: 'Red' | 'Yellow' | 'Green' = 'Green';
}

// File: src/app/components/status-card/status-card.component.html
<mat-card>
  <mat-card-title>{{ endpoint }}</mat-card-title>
  <mat-card-content>
    <span [ngStyle]="{color: statusColor}">{{ status }}</span>
  </mat-card-content>
</mat-card>

// File: src/app/components/status-card/status-card.component.css
span {
  font-weight: bold;
  font-size: 1.2em;
}

// File: src/app/components/status-card/status-card.component.ts (add getter)
get statusColor() {
  switch (this.status) {
    case 'Red': return 'red';
    case 'Yellow': return 'orange';
    case 'Green': return 'green';
    default: return 'black';
  }
}

// File: src/app/components/notification-settings/notification-settings.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-notification-settings',
  template: `<p>Configure email, RSS, or other alerts here.</p>`
})
export class NotificationSettingsComponent {}

// File: src/app/components/self-heal/self-heal.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-self-heal',
  template: `<p>Self-healing actions setup interface.</p>`
})
export class SelfHealComponent {}

// File: styles.css
@import "@angular/material/prebuilt-themes/indigo-pink.css";
body {
  margin: 0;
  font-family: Roboto, sans-serif;
  background: #f4f6f8;
}
.dashboard {
  display: flex;
  gap: 1rem;
  padding: 1rem;
}

// File: tsconfig.json
// [Standard Angular TypeScript config]

// File: package.json
// [Add Angular Material, Animations, and HttpClient via ng add @angular/material]
