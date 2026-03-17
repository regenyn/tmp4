import java.awt.*;
import java.awt.event.*;
import java.util.concurrent.ThreadLocalRandom;

public class jt2 {

    public static boolean cl = true;

    public static void main(String[] args) {
        try {
            Robot robot = new Robot();
            long nextUpTime = System.currentTimeMillis() + 67000L;
            long nextDownTime = System.currentTimeMillis() + 71000L;
            long nextLeftTime = System.currentTimeMillis() + 32000L;
            long nextRightTime = System.currentTimeMillis() + 37000L;
            long nextScrollDownTime = System.currentTimeMillis() + 121000L;
            long nextScrollUpTime = System.currentTimeMillis() + 134000L;
            long nextClickTime = System.currentTimeMillis() + 10000L;
            int upCount = 0;
            int downCount = 0;
            int leftCount = 0;
            int rightCount = 0;
            int scrollDownCount = 0;
            int scrollUpCount = 0;

            while (cl) {
                long now = System.currentTimeMillis();

                boolean upDue = now >= nextUpTime;
                boolean downDue = now >= nextDownTime;
                boolean leftDue = now >= nextLeftTime;
                boolean rightDue = now >= nextRightTime;
                boolean scrollDownDue = now >= nextScrollDownTime;
                boolean scrollUpDue = now >= nextScrollUpTime;

                int dueCount = 0;
                if (upDue) dueCount++;
                if (downDue) dueCount++;
                if (leftDue) dueCount++;
                if (rightDue) dueCount++;
                if (scrollDownDue) dueCount++;
                if (scrollUpDue) dueCount++;

                if (dueCount >= 2) {
                    int seen = 0;

                    if (upDue) {
                        seen++;
                    }

                    if (downDue) {
                        if (dueCount == 2 && seen == 1) {
                            nextDownTime += 1000L;
                            downDue = false;
                        } else if (dueCount == 3) {
                            nextDownTime += (seen == 1) ? 2000L : 4000L;
                            downDue = false;
                        } else if (dueCount == 4) {
                            nextDownTime += 1000L;
                            downDue = false;
                        }
                        seen++;
                    }

                    if (leftDue) {
                        if (dueCount == 2 && seen == 1) {
                            nextLeftTime += 1000L;
                            leftDue = false;
                        } else if (dueCount == 3) {
                            nextLeftTime += (seen == 1) ? 2000L : 4000L;
                            leftDue = false;
                        } else if (dueCount == 4) {
                            nextLeftTime += 3000L;
                            leftDue = false;
                        }
                        seen++;
                    }

                    if (rightDue) {
                        if (dueCount == 2 && seen == 1) {
                            nextRightTime += 1000L;
                            rightDue = false;
                        } else if (dueCount == 3) {
                            nextRightTime += (seen == 1) ? 2000L : 4000L;
                            rightDue = false;
                        } else if (dueCount >= 4) {
                            nextRightTime += 7000L;
                            rightDue = false;
                        }
                        seen++;
                    }

                    if (scrollDownDue) {
                        if (dueCount == 2 && seen == 1) {
                            nextScrollDownTime += 1000L;
                            scrollDownDue = false;
                        } else if (dueCount == 3) {
                            nextScrollDownTime += (seen == 1) ? 2000L : 4000L;
                            scrollDownDue = false;
                        } else if (dueCount >= 4) {
                            nextScrollDownTime += 9000L;
                            scrollDownDue = false;
                        }
                        seen++;
                    }

                    if (scrollUpDue) {
                        if (dueCount == 2 && seen == 1) {
                            nextScrollUpTime += 1000L;
                            scrollUpDue = false;
                        } else if (dueCount == 3) {
                            nextScrollUpTime += (seen == 1) ? 2000L : 4000L;
                            scrollUpDue = false;
                        } else if (dueCount >= 4) {
                            nextScrollUpTime += 11000L;
                            scrollUpDue = false;
                        }
                        seen++;
                    }
                }

                if (upDue) {
                    upCount++;
                    int presses = (upCount % 2 == 1) ? 3 : 5; // odd: 3, even: 5
                    pressKeyTimes(robot, KeyEvent.VK_UP, presses);
                    nextUpTime += 67000L;
                }

                if (downDue) {
                    downCount++;
                    int presses = (downCount % 2 == 1) ? 5 : 3; // odd: 5, even: 3
                    pressKeyTimes(robot, KeyEvent.VK_DOWN, presses);
                    nextDownTime += 71000L;
                }

                if (leftDue) {
                    leftCount++;
                    int presses = (leftCount % 2 == 1) ? 3 : 5; // odd: 3, even: 5
                    pressKeyTimes(robot, KeyEvent.VK_LEFT, presses);
                    nextLeftTime += 32000L;
                }

                if (rightDue) {
                    rightCount++;
                    int presses = (rightCount % 2 == 1) ? 5 : 3; // odd: 5, even: 3
                    pressKeyTimes(robot, KeyEvent.VK_RIGHT, presses);
                    nextRightTime += 37000L;
                }

                if (scrollDownDue) {
                    scrollDownCount++;
                    int notches = (scrollDownCount % 2 == 1) ? 4 : 5; // odd: 4, even: 5
                    scrollTimes(robot, notches);
                    nextScrollDownTime += 121000L;
                }

                if (scrollUpDue) {
                    scrollUpCount++;
                    int notches = (scrollUpCount % 2 == 1) ? 3 : 6; // odd: 3, even: 6
                    scrollTimes(robot, -notches);
                    nextScrollUpTime += 134000L;
                }

                if (now >= nextClickTime) {
                    robot.mousePress(InputEvent.BUTTON1_DOWN_MASK);
                    robot.mouseRelease(InputEvent.BUTTON1_DOWN_MASK);
                    System.out.println("");
                    nextClickTime += 10000L;
                }

                Thread.sleep(50);
            }

        } catch (AWTException | InterruptedException e) {
            e.printStackTrace();
        }
    }

    private static void pressKeyTimes(Robot robot, int keyCode, int times) {
        for (int i = 0; i < times; i++) {
            robot.keyPress(keyCode);
            robot.keyRelease(keyCode);
            try {
                Thread.sleep(ThreadLocalRandom.current().nextInt(60, 121));
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                return;
            }
        }
    }

    private static void scrollTimes(Robot robot, int notches) {
        int steps = Math.abs(notches);
        int direction = notches >= 0 ? 1 : -1;
        for (int i = 0; i < steps; i++) {
            robot.mouseWheel(direction);
            try {
                Thread.sleep(ThreadLocalRandom.current().nextInt(60, 121));
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                return;
            }
        }
    }
}
