
~~~
lazyguy/
├── README.md
├── .gitignore
├── .env
├── docker-compose.yml
├── docker-compose.prod.yml
├── Makefile
├── turbo.json
├── pnpm-workspace.yaml
├── package.json
│
├── proto/                                      ← Shared .proto source files
│   ├── buf.yaml                                ← Buf CLI config
│   ├── buf.gen.yaml                            ← Code generation config
│   ├── auth.proto
│   ├── user.proto
│   ├── tasks.proto
│   ├── sessions.proto
│   ├── stats.proto
│   ├── streak.proto
│   ├── music.proto
│   └── notifications.proto
│
├── client/
│   ├── desktop-app/                                ← Electron 29 Desktop App
│   │   ├── package.json
│   │   ├── tsconfig.json
│   │   ├── electron-builder.yml                ← Build config: Windows, Mac, Linux
│   │   ├── main/
│   │   │   ├── main.ts                         ← Electron main process + BrowserWindow
│   │   │   ├── preload.ts                      ← Context bridge (safe IPC to renderer)
│   │   │   ├── tray.ts                         ← System tray icon + context menu
│   │   │   ├── pip.ts                          ← Always-on-top PiP BrowserWindow
│   │   │   ├── updater.ts                      ← electron-updater auto-update
│   │   │   └── ipc/
│   │   │       ├── timer.ts                    ← IPC: start/pause/skip timer from tray
│   │   │       ├── music.ts                    ← IPC: play/pause/volume from PiP
│   │   │       └── notifications.ts            ← IPC: OS native notifications
│   │   └── resources/
│   │       ├── icon.png
│   │       ├── icon.ico
│   │       ├── icon.icns
│   │       └── tray-icon.png
│   │
│   └── web-app/                                     ← Next.js 14 Frontend
│       ├── package.json
│       ├── next.config.ts
│       ├── tailwind.config.ts
│       ├── tsconfig.json
│       ├── postcss.config.js
│       ├── .env.local
│       │
│       ├── app/
│       │   ├── layout.tsx                      ← Root layout + providers
│       │   ├── globals.css                     ← CSS vars + Tailwind base
│       │   ├── not-found.tsx
│       │   ├── loading.tsx
│       │   ├── error.tsx
│       │   │
│       │   ├── (auth)/
│       │   │   ├── layout.tsx
│       │   │   ├── login/
│       │   │   │   └── page.tsx
│       │   │   ├── register/
│       │   │   │   └── page.tsx
│       │   │   └── forgot-password/
│       │   │       └── page.tsx
│       │   │
│       │   ├── (dashboard)/
│       │   │   ├── layout.tsx                  ← Dashboard shell (modes)
│       │   │   └── page.tsx                    ← Main dashboard (Home/Focus/Ambient)
│       │   │
│       │   ├── (marketing)/
│       │   │   ├── layout.tsx
│       │   │   ├── page.tsx                    ← Landing page
│       │   │   ├── pricing/
│       │   │   │   └── page.tsx
│       │   │   ├── features/
│       │   │   │   ├── page.tsx
│       │   │   │   ├── focus-timer/
│       │   │   │   │   └── page.tsx
│       │   │   │   ├── themes/
│       │   │   │   │   └── page.tsx
│       │   │   │   ├── tasks/
│       │   │   │   │   └── page.tsx
│       │   │   │   ├── soundscapes/
│       │   │   │   │   └── page.tsx
│       │   │   │   ├── stats/
│       │   │   │   │   └── page.tsx
│       │   │   │   └── music/
│       │   │   │       └── page.tsx
│       │   │   ├── blog/
│       │   │   │   ├── page.tsx
│       │   │   │   └── [slug]/
│       │   │   │       └── page.tsx
│       │   │   ├── newsletter/
│       │   │   │   └── page.tsx
│       │   │   └── contact/
│       │   │       └── page.tsx
│       │   │
│       │   └── api/
│       │       ├── auth/
│       │       │   └── [...nextauth]/
│       │       │       └── route.ts            ← NextAuth handler
│       │       ├── upload/
│       │       │   └── route.ts                ← Theme image upload
│       │       └── ai/
│       │           ├── suggestions/
│       │           │   └── route.ts            ← AI task suggestions
│       │           ├── music-recommend/
│       │           │   └── route.ts            ← AI mood → music
│       │           └── focus-tips/
│       │               └── route.ts            ← AI tip of session
│       │
│       ├── components/
│       │   ├── ui/                              ← Base design system
│       │   │   ├── Button.tsx
│       │   │   ├── Toggle.tsx
│       │   │   ├── Slider.tsx
│       │   │   ├── Modal.tsx
│       │   │   ├── Tooltip.tsx
│       │   │   ├── Dropdown.tsx
│       │   │   ├── Badge.tsx
│       │   │   ├── Input.tsx
│       │   │   ├── Select.tsx
│       │   │   ├── Tabs.tsx
│       │   │   ├── Card.tsx
│       │   │   ├── Avatar.tsx
│       │   │   ├── Skeleton.tsx
│       │   │   ├── Progress.tsx
│       │   │   ├── Confetti.tsx
│       │   │   └── ProGate.tsx                 ← Blur overlay + upgrade prompt
│       │   │
│       │   ├── layout/
│       │   │   ├── DashboardShell.tsx          ← Home / Focus / Ambient mode wrapper
│       │   │   ├── BottomDock.tsx              ← Bottom-left: Tasks, Music, Notepad
│       │   │   ├── BottomBar.tsx               ← Bottom-right: streak, home, focus, ambient, gift, settings, fullscreen
│       │   │   ├── ModeBackground.tsx          ← Renders gradient/image/video bg per mode
│       │   │   └── TopBar.tsx                  ← Quote top-right + register banner
│       │   │
│       │   ├── timer/
│       │   │   ├── PomodoroTimer.tsx           ← Orchestrates full timer logic
│       │   │   ├── TimerDisplay.tsx            ← MM:SS big display
│       │   │   ├── TimerControls.tsx           ← Start / Pause / Skip / Reset
│       │   │   ├── FlipClock.tsx               ← Flip animation clock (Plus)
│       │   │   ├── TimerProgress.tsx           ← Progress bar beneath timer (Plus)
│       │   │   ├── SessionTally.tsx            ← Tally icons per session
│       │   │   ├── ModeSelector.tsx            ← Focus / Short Break / Long Break tabs
│       │   │   ├── AlertSound.tsx              ← End-of-session sound picker
│       │   │   └── CountdownTimer.tsx          ← Stopwatch / Countdown mode
│       │   │
│       │   ├── pip/
│       │   │   ├── PipWindow.tsx               ← Document PiP window manager
│       │   │   ├── PipControls.tsx             ← Timer start/pause/skip in PiP
│       │   │   ├── PipMusicPlayer.tsx          ← Music play/pause/volume in PiP
│       │   │   └── PipTaskView.tsx             ← Current task shown in PiP
│       │   │
│       │   ├── tasks/
│       │   │   ├── TaskPanel.tsx               ← Floating task panel popup
│       │   │   ├── TaskItem.tsx                ← Single task row (drag, check, edit, delete)
│       │   │   ├── TaskForm.tsx                ← Add / edit task form
│       │   │   ├── TaskProgress.tsx            ← Tasks completion progress bar
│       │   │   ├── TaskETA.tsx                 ← ETA duration picker (Plus)
│       │   │   ├── TaskEmoji.tsx               ← Emoji picker for task (Plus)
│       │   │   ├── TaskColorTag.tsx            ← Color tag picker (Plus)
│       │   │   ├── TaskConfetti.tsx            ← Confetti when all tasks done
│       │   │   └── TaskDragList.tsx            ← @hello-pangea/dnd drag list
│       │   │
│       │   ├── music/
│       │   │   ├── MusicPanel.tsx              ← Full panel: Sounds / My Music / Playlists tabs
│       │   │   ├── AmbientSounds.tsx           ← Layerable ambient sound grid
│       │   │   ├── SoundCard.tsx               ← Single sound card with volume
│       │   │   ├── SoundLayerMixer.tsx         ← Mix multiple sounds simultaneously
│       │   │   ├── PlaylistLibrary.tsx         ← Curated + user playlists
│       │   │   ├── CustomPlaylistForm.tsx      ← Add Spotify / YouTube / SoundCloud URL
│       │   │   ├── FavoritesList.tsx           ← Pinned favorites (shown in PiP too)
│       │   │   ├── MiniPlayer.tsx              ← Mini player in bottom dock
│       │   │   ├── SpotifyPlayer.tsx           ← Spotify Web Playback SDK
│       │   │   ├── YouTubePlayer.tsx           ← YouTube IFrame API
│       │   │   ├── SoundCloudPlayer.tsx        ← SoundCloud Widget API
│       │   │   ├── AppleMusicPlayer.tsx        ← MusicKit JS
│       │   │   └── MusicSearch.tsx             ← Search across platforms
│       │   │
│       │   ├── themes/
│       │   │   ├── ThemePanel.tsx              ← Theme settings panel
│       │   │   ├── ThemeCard.tsx               ← Single theme preview card
│       │   │   ├── ThemeLibrary.tsx            ← Type/Environment/Color filtered grid
│       │   │   ├── GradientBackground.tsx      ← CSS gradient renderer
│       │   │   ├── VideoBackground.tsx         ← YouTube iframe background (Plus)
│       │   │   ├── ImageBackground.tsx         ← Custom uploaded image bg (Plus)
│       │   │   └── OverlaySlider.tsx           ← Opacity overlay control
│       │   │
│       │   ├── stats/
│       │   │   ├── FocusStats.tsx              ← Stats panel container
│       │   │   ├── StatsCards.tsx              ← Streak / Focus Time / Score / Tasks / Sessions / Break
│       │   │   ├── ProductivityChart.tsx       ← Recharts line graph
│       │   │   ├── FocusScore.tsx              ← Score calculation + display (Plus)
│       │   │   └── StatsExport.tsx             ← Export stats as CSV/PDF
│       │   │
│       │   ├── notepad/
│       │   │   ├── Notepad.tsx                 ← Tiptap rich text editor
│       │   │   ├── NotepadToolbar.tsx          ← Bold/Italic/H1/H2/Lists/Align toolbar
│       │   │   └── WordCount.tsx               ← Word + char counter (Plus)
│       │   │
│       │   ├── ai/
│       │   │   ├── AIAssistant.tsx             ← AI chat panel (floating)
│       │   │   ├── TaskSuggestions.tsx         ← AI suggested tasks
│       │   │   ├── MusicRecommend.tsx          ← AI mood → music picker
│       │   │   ├── FocusTips.tsx               ← AI focus tip per session
│       │   │   └── AIFloatingButton.tsx        ← Floating AI trigger button
│       │   │
│       │   ├── settings/
│       │   │   ├── SettingsPanel.tsx           ← Sidebar + content area
│       │   │   ├── ClockSettings.tsx           ← 12h/24h, flip, seconds, greetings, font
│       │   │   ├── TimerSettings.tsx           ← Mode, lengths, tally, alert, auto-start
│       │   │   ├── QuotesSettings.tsx          ← Category, show in focus/home
│       │   │   ├── ExtrasSettings.tsx          ← Name, animations, clear mode, prevent sleep, share button
│       │   │   ├── AccountSettings.tsx         ← Create / sign in / manage account
│       │   │   ├── StatsSettings.tsx           ← Stats visibility + reset
│       │   │   ├── SupportSettings.tsx         ← Help, feedback, contact, Discord link
│       │   │   └── WhatsNew.tsx               ← Changelog viewer
│       │   │
│       │   ├── quotes/
│       │   │   └── QuoteDisplay.tsx            ← Motivational quote top-right
│       │   │
│       │   ├── clock/
│       │   │   ├── ClockDisplay.tsx            ← Home mode analog/digital clock
│       │   │   ├── GreetingText.tsx            ← "Good morning, [name]"
│       │   │   └── FlipClockHome.tsx           ← Flip clock for home mode (Plus)
│       │   │
│       │   ├── notifications/
│       │   │   ├── ToastNotification.tsx       ← react-hot-toast wrapper
│       │   │   ├── TimerAlert.tsx              ← Browser notification on timer end
│       │   │   └── StreakToast.tsx             ← "You're on a X day streak" popup
│       │   │
│       │   ├── pricing/
│       │   │   ├── PricingPage.tsx             ← Free vs Pro plan comparison
│       │   │   ├── PricingCard.tsx             ← Single plan card
│       │   │   └── UpgradeModal.tsx            ← In-app upgrade prompt modal
│       │   │
│       │   └── marketing/
│       │       ├── HeroSection.tsx
│       │       ├── FeaturesGrid.tsx
│       │       ├── FeedbackSection.tsx
│       │       ├── TestimonialsSection.tsx
│       │       ├── TrustedBySection.tsx        ← NYU, Harvard, Netflix, Spotify, Adobe, Amazon logos
│       │       ├── MarketingNav.tsx
│       │       ├── MarketingFooter.tsx
│       │       └── NewsletterCTA.tsx
│       │
│       ├── hooks/
│       │   ├── useTimer.ts                     ← Core countdown logic
│       │   ├── usePomodoroSession.ts           ← Pomodoro cycle manager (focus→break→focus)
│       │   ├── useAmbientSound.ts              ← Howler.js sound manager + layering
│       │   ├── useTasks.ts                     ← Task CRUD + optimistic sync
│       │   ├── useTheme.ts                     ← Theme apply + persist per mode
│       │   ├── useStats.ts                     ← Stats fetch + compute
│       │   ├── useStreak.ts                    ← Streak check + update
│       │   ├── useAI.ts                        ← AI API calls with streaming
│       │   ├── usePiP.ts                       ← Document Picture-in-Picture API
│       │   ├── useKeyboardShortcuts.ts         ← Global keyboard shortcuts
│       │   ├── useFullscreen.ts                ← Fullscreen toggle
│       │   ├── useMediaSession.ts              ← Browser Media Session API (lock screen controls)
│       │   ├── useMusic.ts                     ← Music state + controls
│       │   ├── useSpotify.ts                   ← Spotify Web Playback SDK
│       │   ├── useNotification.ts              ← Browser push notifications
│       │   ├── useAuth.ts                      ← Auth state helpers
│       │   └── useSettings.ts                  ← Settings read/write helpers
│       │
│       ├── stores/
│       │   ├── timerStore.ts                   ← mode, timeLeft, isRunning, sessionCount, tally
│       │   ├── taskStore.ts                    ← tasks[], activeTaskId, completedToday
│       │   ├── musicStore.ts                   ← activeSounds, playlist, volume, currentPlatform
│       │   ├── themeStore.ts                   ← homeTheme, focusTheme, ambientTheme
│       │   ├── statsStore.ts                   ← focusTime, sessions, streak, score
│       │   ├── userStore.ts                    ← user, isPro, preferences
│       │   ├── settingsStore.ts                ← clock, timer, quotes, extras settings
│       │   └── uiStore.ts                      ← openPanel, currentMode, isPipOpen
│       │
│       ├── lib/
│       │   ├── api-client.ts                   ← Axios instance pointing to Go server
│       │   ├── grpc-client.ts                  ← ConnectRPC client setup
│       │   ├── auth.ts                         ← NextAuth config + callbacks
│       │   ├── ai.ts                           ← OpenAI client (Node.js SDK)
│       │   ├── stripe.ts                       ← Stripe.js client
│       │   ├── firebase.ts                     ← Firebase client SDK init
│       │   ├── utils.ts                        ← cn(), formatTime(), debounce()
│       │   ├── quotes.ts                       ← 300+ motivational quotes array
│       │   ├── themes.ts                       ← All theme definitions + metadata
│       │   ├── sounds.ts                       ← All ambient sound definitions
│       │   ├── changelog.ts                    ← What's New entries
│       │   └── validations.ts                  ← Zod schemas
│       │
│       ├── types/
│       │   ├── timer.ts
│       │   ├── task.ts
│       │   ├── user.ts
│       │   ├── music.ts
│       │   ├── stats.ts
│       │   ├── theme.ts
│       │   ├── ai.ts
│       │   ├── pip.ts
│       │   └── next-auth.d.ts                  ← Session type extension
│       │
│       ├── generated/                          ← Auto-generated from proto (DO NOT EDIT)
│       │   └── proto/
│       │       ├── auth_pb.ts
│       │       ├── auth-AuthService_connectquery.ts
│       │       ├── tasks_pb.ts
│       │       ├── tasks-TaskService_connectquery.ts
│       │       ├── sessions_pb.ts
│       │       ├── sessions-SessionService_connectquery.ts
│       │       ├── stats_pb.ts
│       │       ├── stats-StatsService_connectquery.ts
│       │       ├── streak_pb.ts
│       │       ├── streak-StreakService_connectquery.ts
│       │       └── user_pb.ts
│       │
│       ├── middleware                       ← Auth middleware (protected routes)
│       |   └── middleware.ts
│       │
│       └── public/
│           ├── favicon.ico
│           ├── logo.svg
│           ├── logo-dark.svg
│           ├── og-image.png
│           ├── manifest.json
│           ├── sounds/                         ← Alert / notification sounds
│           │   ├── sparkle.mp3
│           │   ├── chime.mp3
│           │   ├── success.mp3
│           │   ├── applause.mp3
│           │   ├── train-arrival.mp3
│           │   ├── game-show.mp3
│           │   ├── soft.mp3
│           │   ├── piano.mp3
│           │   ├── level-up.mp3
│           │   ├── airport.mp3
│           │   └── commuter-jingle.mp3
│           ├── ambient/                        ← Loopable ambient sounds
│           │   ├── rain.mp3
│           │   ├── ocean.mp3
│           │   ├── cafe.mp3
│           │   ├── airplane-cabin.mp3
│           │   ├── exam-hall.mp3
│           │   ├── fireplace.mp3
│           │   ├── thunderstorm.mp3
│           │   ├── white-noise.mp3
│           │   ├── pink-noise.mp3
│           │   ├── brown-noise.mp3
│           │   ├── wind.mp3
│           │   ├── campfire.mp3
│           │   ├── office.mp3
│           │   ├── nyc-morning.mp3
│           │   ├── commuter-train.mp3
│           │   ├── japanese-library.mp3
│           │   ├── light-rain.mp3
│           │   ├── heavy-rain.mp3
│           │   ├── binaural-gamma.mp3
│           │   ├── binaural-beta.mp3
│           │   ├── binaural-alpha.mp3
│           │   ├── binaural-theta.mp3
│           │   ├── binaural-delta.mp3
│           │   ├── street-cafe.mp3
│           │   └── countryside-morning.mp3
│           └── themes/                         ← Theme background images
│               ├── aura-twilight.jpg
│               ├── peach-aura-heart.jpg
│               ├── light-pink-heart.jpg
│               ├── flare.jpg
│               ├── minimalist-black.jpg
│               ├── minimalist-white.jpg
│               ├── blue-flare.jpg
│               ├── lava-lamp.gif
│               ├── pink-flare.jpg
│               ├── rainbow-flare.jpg
│               ├── dark-flare.jpg
│               ├── snowy-cabin.jpg
│               ├── tokyo-night.jpg
│               ├── forest.jpg
│               ├── sunset.jpg
│               └── gradient-purple.jpg
│
└── server/                                  ← Go 1.22 Backend (REST + gRPC)
    ├── go.mod
    ├── go.sum
    ├── Makefile
    ├── Dockerfile
    ├── .env
    ├── .air.toml                               ← Air live-reload config
    │
    ├── cmd/
    │   └── api/
    │       └── main.go                         ← Entry point: starts REST + gRPC servers
    │
    ├── config/
    │   ├── config.go                           ← Viper config loader
    │   └── config.yaml                         ← Default config values
    │
    ├── internal/
    │   ├── auth/
    │   │   ├── handler.go                      ← REST: POST /auth/register, /login, /refresh, /logout
    │   │   ├── grpc_handler.go                 ← gRPC: AuthService
    │   │   ├── service.go                      ← Business logic: register, login, token refresh
    │   │   ├── repository.go                   ← DB: user lookup, token storage
    │   │   ├── middleware.go                   ← JWT validation middleware
    │   │   └── dto.go                          ← RegisterReq, LoginReq, TokenRes
    │   │
    │   ├── user/
    │   │   ├── handler.go                      ← REST: GET/PATCH /user, GET /user/pro-status
    │   │   ├── grpc_handler.go                 ← gRPC: UserService
    │   │   ├── service.go
    │   │   ├── repository.go
    │   │   └── dto.go
    │   │
    │   ├── tasks/
    │   │   ├── handler.go                      ← REST: CRUD /tasks, /tasks/:id
    │   │   ├── grpc_handler.go                 ← gRPC: TaskService (streaming sync)
    │   │   ├── service.go                      ← create, update, delete, reorder, complete
    │   │   ├── repository.go
    │   │   └── dto.go
    │   │
    │   ├── sessions/
    │   │   ├── handler.go                      ← REST: POST /sessions, GET /sessions/stats
    │   │   ├── grpc_handler.go                 ← gRPC: SessionService (stream timer events)
    │   │   ├── service.go                      ← save session, compute daily stats
    │   │   ├── repository.go
    │   │   └── dto.go
    │   │
    │   ├── stats/
    │   │   ├── handler.go                      ← REST: GET /stats?period=today|week|month
    │   │   ├── grpc_handler.go                 ← gRPC: StatsService
    │   │   ├── service.go                      ← aggregate focus time, score calc
    │   │   ├── repository.go
    │   │   └── dto.go
    │   │
    │   ├── streak/
    │   │   ├── handler.go                      ← REST: GET /streak, POST /streak/check
    │   │   ├── grpc_handler.go                 ← gRPC: StreakService
    │   │   ├── service.go                      ← daily streak logic, reset detection
    │   │   ├── repository.go
    │   │   └── dto.go
    │   │
    │   ├── music/
    │   │   ├── handler.go                      ← REST: GET /music/playlists, POST /music/favorites
    │   │   ├── service.go                      ← favorites CRUD, playlist management
    │   │   ├── repository.go
    │   │   └── dto.go
    │   │
    │   ├── themes/
    │   │   ├── handler.go                      ← REST: GET /themes, POST /themes/upload, PATCH /themes/user
    │   │   ├── service.go
    │   │   ├── repository.go
    │   │   └── dto.go
    │   │
    │   ├── newsletter/
    │   │   ├── handler.go                      ← REST: POST /newsletter/subscribe, GET /newsletter/posts
    │   │   ├── service.go
    │   │   ├── repository.go                   ← MongoDB: posts, subscribers
    │   │   └── dto.go
    │   │
    │   ├── payments/
    │   │   ├── handler.go                      ← REST: POST /payments/checkout, POST /payments/webhook
    │   │   ├── service.go
    │   │   ├── repository.go
    │   │   ├── stripe.go                       ← Stripe checkout, webhook verify, subscription mgmt
    │   │   └── dto.go
    │   │
    │   └── notifications/
    │       ├── handler.go                      ← REST: POST /notifications/register-token
    │       ├── service.go                      ← FCM send, streak reminders, timer alerts
    │       └── firebase.go                     ← Firebase Admin SDK push notification
    │
    ├── pkg/
    │   ├── database/
    │   │   ├── postgres.go                     ← pgx/v5 pool singleton
    │   │   └── migrations/
    │   │       ├── 000001_create_users.up.sql
    │   │       ├── 000001_create_users.down.sql
    │   │       ├── 000002_create_tasks.up.sql
    │   │       ├── 000002_create_tasks.down.sql
    │   │       ├── 000003_create_sessions.up.sql
    │   │       ├── 000003_create_sessions.down.sql
    │   │       ├── 000004_create_stats.up.sql
    │   │       ├── 000004_create_stats.down.sql
    │   │       ├── 000005_create_streaks.up.sql
    │   │       ├── 000005_create_streaks.down.sql
    │   │       ├── 000006_create_payments.up.sql
    │   │       ├── 000006_create_payments.down.sql
    │   │       ├── 000007_create_user_themes.up.sql
    │   │       ├── 000007_create_user_themes.down.sql
    │   │       ├── 000008_create_music_favorites.up.sql
    │   │       └── 000008_create_music_favorites.down.sql
    │   │
    │   ├── models/                         ← Go structs (SQLC or pgx scan targets)
    │   │   ├── user.go
    │   │   ├── task.go
    │   │   ├── session.go
    │   │   ├── stats.go
    │   │   ├── streak.go
    │   │   ├── payment.go
    │   │   ├── user_theme.go
    │   │   └── music_favorite.go
    │   │
    │   ├── redis/
    │   │   ├── client.go                       ← go-redis/v9 client singleton
    │   │   ├── cache.go                        ← Set/Get/Del with TTL helpers
    │   │   └── pubsub.go                       ← Pub/Sub for real-time timer sync
    │   │
    │   ├── mongodb/
    │   │   ├── client.go                       ← mongo-driver client singleton
    │   │   └── collections/
    │   │       ├── newsletter.go               ← Newsletter posts, subscribers
    │   │       ├── search_logs.go              ← Search query logs
    │   │       └── analytics.go                ← Event analytics
    │   │
    │   ├── firebase/
    │   │   ├── client.go                       ← firebase-admin-go init
    │   │   └── push.go                         ← FCM send notification helper
    │   │
    │   ├── storage/
    │   │   ├── s3.go                           ← AWS S3 / Cloudflare R2 upload
    │   │   └── local.go                        ← Local file storage (dev)
    │   │
    │   ├── middleware/
    │   │   ├── auth.go                         ← JWT Bearer token middleware
    │   │   ├── cors.go                         ← CORS config
    │   │   ├── rate_limit.go                   ← Redis-backed rate limiter
    │   │   ├── logger.go                       ← zap structured request logging
    │   │   └── recovery.go                     ← Panic recovery
    │   │
    │   └── utils/
    │       ├── jwt.go                          ← Issue / verify JWT tokens
    │       ├── hash.go                         ← bcrypt password hash
    │       ├── response.go                     ← Standardized JSON response helpers
    │       ├── validator.go                    ← go-playground/validator setup
    │       └── time.go                         ← Time helpers + timezone utils
    │
    ├── api/
    │   ├── rest/
    │   │   └── router.go                       ← Gin router: all routes + middleware chain
    │   └── grpc/
    │       └── server.go                       ← gRPC server: register all services + interceptors
    │
    └── proto/                              ← Auto-generated Go gRPC code (DO NOT EDIT)
        ├── auth/
        │   ├── auth.pb.go
        │   └── auth_grpc.pb.go
        ├── user/
        │   ├── user.pb.go
        │   └── user_grpc.pb.go
        ├── tasks/
        │   ├── tasks.pb.go
        │   └── tasks_grpc.pb.go
        ├── sessions/
        │   ├── sessions.pb.go
        │   └── sessions_grpc.pb.go
        ├── stats/
        │   ├── stats.pb.go
        │   └── stats_grpc.pb.go
        ├── streak/
        │   ├── streak.pb.go
        │   └── streak_grpc.pb.go
        └── notifications/
            ├── notifications.pb.go
            └── notifications_grpc.pb.go
~~
