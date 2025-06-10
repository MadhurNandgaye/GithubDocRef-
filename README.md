=== ANGULAR FRONTEND PROJECT STRUCTURE ===

logic-app-monitor-ui/
├── angular.json
├── package.json
├── tsconfig.json
├── src/
│   ├── index.html
│   ├── main.ts
│   ├── styles.css
│   ├── app/
│   │   ├── app.module.ts
│   │   ├── app-routing.module.ts
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

=== FILE CONTENTS ===

// index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>Logic App Monitor</title>
  <base href="/" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
</head>
<body>
  <app-root></app-root>
</body>
</html>

// main.ts
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app/app.module';
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));

// styles.css
@import "@angular/material/prebuilt-themes/indigo-pink.css";
body {
  margin: 0;
  font-family: Roboto, sans-serif;
  background-color: #f5f5f5;
}

// app.component.ts
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
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

// app-routing.module.ts
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
const routes: Routes = [];
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}

// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { HttpClientModule } from '@angular/common/http';
import { AppRoutingModule } from './app-routing.module';
import { MatToolbarModule } from '@angular/material/toolbar';
import { MatCardModule } from '@angular/material/card';
import { MatIconModule } from '@angular/material/icon';
import { MatButtonModule } from '@angular/material/button';
import { MatSnackBarModule } from '@angular/material/snack-bar';

import { AppComponent } from './app.component';
import { DashboardComponent } from './components/dashboard/dashboard.component';
import { EndpointStatusComponent } from './components/endpoint-status/endpoint-status.component';
import { NotificationsComponent } from './components/notifications/notifications.component';
import { ActionsComponent } from './components/actions/actions.component';

@NgModule({
  declarations: [
    AppComponent,
    DashboardComponent,
    EndpointStatusComponent,
    NotificationsComponent,
    ActionsComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    HttpClientModule,
    AppRoutingModule,
    MatToolbarModule,
    MatCardModule,
    MatIconModule,
    MatButtonModule,
    MatSnackBarModule
  ],
  bootstrap: [AppComponent]
})
export class AppModule {}

// models/endpoint.model.ts
export interface Endpoint {
  name: string;
  status: 'Red' | 'Yellow' | 'Green';
  responseTime: number;
  lastChecked: Date;
}

// services/monitor.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';
import { Endpoint } from '../models/endpoint.model';

@Injectable({ providedIn: 'root' })
export class MonitorService {
  constructor(private http: HttpClient) {}

  getEndpointStatus(): Observable<Endpoint[]> {
    return this.http.get<Endpoint[]>('/api/monitor/endpoints');
  }

  triggerAction(endpoint: string): Observable<any> {
    return this.http.post('/api/monitor/actions', { endpoint });
  }
}

// components/dashboard/dashboard.component.ts
import { Component } from '@angular/core';
@Component({
  selector: 'app-dashboard',
  templateUrl: './dashboard.component.html',
  styleUrls: ['./dashboard.component.css']
})
export class DashboardComponent {}

// components/dashboard/dashboard.component.html
<mat-card>
  <mat-card-title>Endpoint Status</mat-card-title>
  <app-endpoint-status></app-endpoint-status>
</mat-card>
<mat-card style="margin-top: 16px;">
  <mat-card-title>Notifications</mat-card-title>
  <app-notifications></app-notifications>
</mat-card>
<mat-card style="margin-top: 16px;">
  <mat-card-title>Self-Heal Actions</mat-card-title>
  <app-actions></app-actions>
</mat-card>

// components/dashboard/dashboard.component.css
mat-card {
  margin-bottom: 16px;
}

// components/endpoint-status/endpoint-status.component.ts
import { Component, OnInit } from '@angular/core';
import { MonitorService } from '../../services/monitor.service';
import { Endpoint } from '../../models/endpoint.model';

@Component({
  selector: 'app-endpoint-status',
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

// components/endpoint-status/endpoint-status.component.html
<div *ngFor="let ep of endpoints">
  <mat-card>
    <mat-card-title>
      {{ ep.name }} - <span [ngClass]="ep.status.toLowerCase()">{{ ep.status }}</span>
    </mat-card-title>
    <mat-card-content>
      Response Time: {{ ep.responseTime }} ms<br/>
      Last Checked: {{ ep.lastChecked | date:'short' }}
    </mat-card-content>
  </mat-card>
</div>

// components/endpoint-status/endpoint-status.component.css
.red { color: red; }
.yellow { color: orange; }
.green { color: green; }

// components/notifications/notifications.component.ts
import { Component } from '@angular/core';
@Component({
  selector: 'app-notifications',
  templateUrl: './notifications.component.html',
  styleUrls: ['./notifications.component.css']
})
export class NotificationsComponent {
  notifications = [
    'API A degraded from external network',
    'UI Service response time above threshold'
  ];
}

// components/notifications/notifications.component.html
<ul>
  <li *ngFor="let note of notifications">
    {{ note }}
  </li>
</ul>

// components/notifications/notifications.component.css
ul {
  padding-left: 20px;
}
li {
  margin-bottom: 8px;
}

// components/actions/actions.component.ts
import { Component } from '@angular/core';
import { MonitorService } from '../../services/monitor.service';
import { MatSnackBar } from '@angular/material/snack-bar';

@Component({
  selector: 'app-actions',
  templateUrl: './actions.component.html',
  styleUrls: ['./actions.component.css']
})
export class ActionsComponent {
  constructor(private monitorService: MonitorService, private snackBar: MatSnackBar) {}

  triggerSelfHeal() {
    this.monitorService.triggerAction('API A').subscribe(() => {
      this.snackBar.open('Self-heal triggered for API A', 'Close', { duration: 3000 });
    });
  }
}

// components/actions/actions.component.html
<button mat-raised-button color="warn" (click)="triggerSelfHeal()">
  Trigger Self-Heal for API A
</button>

// components/actions/actions.component.css
button {
  margin-top: 10px;
}
