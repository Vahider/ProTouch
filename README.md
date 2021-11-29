# ProTouch

DisplayMetrics displayMetrics = new DisplayMetrics();
        getWindowManager().getDefaultDisplay().getMetrics(displayMetrics);
        // int height = displayMetrics.heightPixels;
        int width = displayMetrics.widthPixels;
        SWIPE_MIN_DISTANCE = width / 7;

        View yyyyy = findViewById(R.id.yyyyy);
        yyyyy.setOnTouchListener((view, event) -> {
            switch (event.getAction()) {
                case MotionEvent.ACTION_DOWN:
                    x1 = event.getX();
                    y1 = event.getY();
                    break;

                case MotionEvent.ACTION_UP:
                    x2 = event.getX();
                    y2 = event.getY();

                    // LR2RL
                    float deltaX = x2 - x1;
                    float deltaY = y2 - y1;
                    if (Math.abs(deltaY) > SWIPE_MIN_DISTANCE) {
                        if (deltaY > 0) {
                            // T2B
                        } else {
                            // B2T
                        }
                    } else if (Math.abs(deltaX) > SWIPE_MIN_DISTANCE) {
                        if (deltaX > 0) {
                            // L2R
                        } else {
                            // R2L
                        }
                    } else if (Math.abs(deltaX + deltaY) < (SWIPE_MIN_DISTANCE / 10)) {
                        long currentClickTime = System.currentTimeMillis();
                        if (currentClickTime - LAST_CLICK_TIME <= DOUBLE_CLICK_INTERVAL) {
                            flagClick = false;
                            // Double Click
                        } else {
                            LAST_CLICK_TIME = System.currentTimeMillis();
                            flagClick = true;
                            App.HANDLER.postDelayed(() -> {
                                if (flagClick) {
                                    // One Click
                                }
                            }, DOUBLE_CLICK_INTERVAL);
                        }
                    }
            }
            return true;
        });
