# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a YouTube Course Creation Web App built with Next.js that allows users to automatically generate structured courses from YouTube videos. The app downloads YouTube videos, extracts transcripts, processes them with Google's Gemini AI to create chapter breakdowns, and generates video clips for each chapter.

## Development Commands

All commands should be run from the `app/` directory:

```bash
cd app/
npm run dev      # Start development server on http://localhost:3000
npm run build    # Build for production
npm run start    # Start production server
npm run lint     # Run ESLint
```

## Architecture

### Core Components

- **Main Page** (`src/app/page.tsx`): Client-side interface with URL input, chapter sidebar, and video player
- **API Route** (`src/app/api/create-course/route.ts`): Server-side processing pipeline that:
  1. Downloads YouTube audio using `ytdl-core`
  2. Fetches transcript with `youtube-transcript`
  3. Processes transcript with Google Gemini AI to generate chapters
  4. Splits video into chapter clips using `fluent-ffmpeg`
  5. Returns structured chapter data with video paths

### UI Components (`src/components/ui/`)

- Simple, reusable components (Button, Input, Sidebar, VideoPlayer, Card)
- Use standard HTML elements with TypeScript interfaces
- Follow React functional component pattern

### Data Flow

1. User submits YouTube URL
2. Frontend calls `/api/create-course` POST endpoint
3. Server downloads video, processes transcript, generates chapters
4. AI returns structured chapters with titles, summaries, and timestamps
5. Video is split into clips stored in `public/clips/`
6. Frontend displays chapters in sidebar with video player

### Key Technologies

- **Next.js 15** with App Router
- **TypeScript** with strict mode
- **Tailwind CSS** for styling
- **Google Gemini AI** for transcript processing
- **FFmpeg** for video manipulation
- **ytdl-core** for YouTube downloads

## Environment Setup

Required environment variables:
- `GOOGLE_API_KEY`: Google Gemini AI API key

## File Structure

- Working directory is in `app/` subdirectory
- TypeScript path alias `@/*` maps to `src/*`
- Video clips stored in `public/clips/`
- Temporary files in `/tmp/`

## Development Notes

- All video processing happens server-side in the API route
- Client-side state managed with React hooks
- Error handling implemented at each processing step
- Video files are temporarily stored and cleaned up