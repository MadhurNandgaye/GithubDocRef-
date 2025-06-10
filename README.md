=== SIMPLE ANGULAR STANDALONE FRONTEND FOR LOGIC APP MONITOR ===

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
│   │   ├── services/
│   │   │   ├── monitor.service.ts
│   │   ├── models/
│   │   │   ├── endpoint.model.ts

// index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Logic App Monitor</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
</head>
<body>
  <app-root></app-root>
</body>
</html>

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

export const appConfig: ApplicationConfig = {
  providers: [
    provideHttpClient(),
    provideAnimations()
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
<mat-toolbar color="primary">Logic App Monitor</mat-toolbar>
<div style="padding: 16px">
  <app-dashboard></app-dashboard>
</div>

// styles.css
@import "@angular/material/prebuilt-themes/indigo-pink.css";
body {
  margin: 0;
  font-family: Roboto, sans-serif;
}

// components/dashboard/dashboard.component.ts
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { MatCardModule } from '@angular/material/card';
import { EndpointStatusComponent } from '../endpoint-status/endpoint-status.component';

@Component({
  selector: 'app-dashboard',
  standalone: true,
  imports: [CommonModule, MatCardModule, EndpointStatusComponent],
  templateUrl: './dashboard.component.html',
  styleUrls: ['./dashboard.component.css']
})
export class DashboardComponent {}

// dashboard.component.html
<mat-card>
  <mat-card-title>Endpoint Health</mat-card-title>
  <mat-card-content>
    <app-endpoint-status></app-endpoint-status>
  </mat-card-content>
</mat-card>

// dashboard.component.css
mat-card {
  margin: 20px;
}

// endpoint-status.component.ts
import { Component, OnInit } from '@angular/core';
import { CommonModule } from '@angular/common';
import { MonitorService } from '../../services/monitor.service';
import { Endpoint } from '../../models/endpoint.model';
import { MatListModule } from '@angular/material/list';
import { MatIconModule } from '@angular/material/icon';

@Component({
  selector: 'app-endpoint-status',
  standalone: true,
  imports: [CommonModule, MatListModule, MatIconModule],
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

// endpoint-status.component.html
<mat-list>
  <mat-list-item *ngFor="let endpoint of endpoints">
    <mat-icon [style.color]="getColor(endpoint.status)">fiber_manual_record</mat-icon>
    {{endpoint.name}} ({{endpoint.status}})
  </mat-list-item>
</mat-list>

// endpoint-status.component.css
mat-icon {
  margin-right: 8px;
}

// services/monitor.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable, of } from 'rxjs';
import { Endpoint } from '../models/endpoint.model';

@Injectable({ providedIn: 'root' })
export class MonitorService {
  constructor(private http: HttpClient) {}
  getEndpointStatus(): Observable<Endpoint[]> {
    return of([
      { name: 'API 1', status: 'Green' },
      { name: 'API 2', status: 'Yellow' },
      { name: 'API 3', status: 'Red' }
    ]);
  }
}

// models/endpoint.model.ts
export interface Endpoint {
  name: string;
  status: 'Green' | 'Yellow' | 'Red';
}

=== END OF SIMPLE COMPLETE FRONTEND ===
