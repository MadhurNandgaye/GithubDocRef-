=== ANGULAR FRONTEND PROJECT STRUCTURE (UPDATED WITH STANDALONE SETUP) ===

logic-app-monitor-ui/
├── angular.json
├── package.json
├── tsconfig.json
├── src/
│   ├── index.html
│   ├── main.ts
│   ├── styles.css
│   ├── app/
│   │   ├── app.config.ts
│   │   ├── app.component.ts
│   │   ├── app.component.html
│   │   ├── components/
│   │   │   ├── dashboard/
│   │   │   │   ├── dashboard.component.ts
│   │   │   │   ├── dashboard.component.html
│   │   │   │   ├── dashboard.component.css
│   │   │   ├── endpoint-status/
│   │   │   │   ├── endpoint-status.component.ts
│   │   │   │   ├── endpoint-status.component.html
│   │   │   │   ├── endpoint-status.component.css
│   │   │   ├── notifications/
│   │   │   │   ├── notifications.component.ts
│   │   │   │   ├── notifications.component.html
│   │   │   │   ├── notifications.component.css
│   │   │   ├── actions/
│   │   │   │   ├── actions.component.ts
│   │   │   │   ├── actions.component.html
│   │   │   │   ├── actions.component.css
│   │   ├── services/
│   │   │   ├── monitor.service.ts
│   │   ├── models/
│   │   │   ├── endpoint.model.ts

=== FILE CONTENTS (UPDATED BOOTSTRAP STYLE) ===

// main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { AppComponent } from './app/app.component';
import { appConfig } from './app/app.config';

bootstrapApplication(AppComponent, appConfig)
  .catch(err => console.error(err));

// app.config.ts
import { ApplicationConfig } from '@angular/core';
import { provideHttpClient } from '@angular/common/http';
import { provideAnimations } from '@angular/platform-browser/animations';
import {
  MatToolbarModule,
  MatCardModule,
  MatIconModule,
  MatButtonModule,
  MatSnackBarModule
} from '@angular/material';

export const appConfig: ApplicationConfig = {
  providers: [
    provideHttpClient(),
    provideAnimations(),
    MatToolbarModule,
    MatCardModule,
    MatIconModule,
    MatButtonModule,
    MatSnackBarModule
  ]
};

// app.component.ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { MatToolbarModule } from '@angular/material/toolbar';
import { DashboardComponent } from './components/dashboard/dashboard.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [CommonModule, MatToolbarModule, DashboardComponent],
  templateUrl: './app.component.html'
})
export class AppComponent {}

// app.component.html
<mat-toolbar color="primary">
  Logic App Monitor
</mat-toolbar>
<div style="padding: 16px">
  <app-dashboard></app-dashboard>
</div>

// All other component files (e.g., dashboard.component.ts) must also be marked as standalone:

// components/dashboard/dashboard.component.ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { EndpointStatusComponent } from '../endpoint-status/endpoint-status.component';
import { NotificationsComponent } from '../notifications/notifications.component';
import { ActionsComponent } from '../actions/actions.component';
import { MatCardModule } from '@angular/material/card';

@Component({
  selector: 'app-dashboard',
  standalone: true,
  imports: [CommonModule, MatCardModule, EndpointStatusComponent, NotificationsComponent, ActionsComponent],
  templateUrl: './dashboard.component.html',
  styleUrls: ['./dashboard.component.css']
})
export class DashboardComponent {}

// Repeat the same pattern (standalone: true, imports: [...]) for:
// - endpoint-status.component.ts
// - notifications.component.ts
// - actions.component.ts

// Example update for endpoint-status.component.ts
import { Component, OnInit } from '@angular/core';
import { CommonModule } from '@angular/common';
import { MonitorService } from '../../services/monitor.service';
import { Endpoint } from '../../models/endpoint.model';
import { MatCardModule } from '@angular/material/card';

@Component({
  selector: 'app-endpoint-status',
  standalone: true,
  imports: [CommonModule, MatCardModule],
  templateUrl: './endpoint-status.component.html',
  styleUrls: ['./endpoint-status.component.css']
})
export class EndpointStatusComponent implements OnInit {
  endpoints: Endpoint[] = [];
  constructor(private monitorService: MonitorService) {}
  ngOnInit() {
    this.monitorService.getEndpointStatus().subscribe(data => this.endpoints = data);
  }
}
