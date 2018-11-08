#include <windows.h>

long WINAPI WndProc(HWND hWnd,UINT iMessage,WPARAM wParam,LPARAM lParam);
BOOL InitWindowsClass(HINSTANCE hInstance);
BOOL InitWindows(HINSTANCE hInstance,int nCmdShow);

HWND hWndMain;
RECT rect1;

int WINAPI WinMain(HINSTANCE hInstance,HINSTANCE hPrevInstance,LPSTR lpCmdLine,int nCmdShow)
{
    MSG Message;
    if(!InitWindowsClass(hInstance))
        return FALSE;
    if(!InitWindows(hInstance,nCmdShow))
        return FALSE;
    while(GetMessage(&Message,0,0,0))
    {
        TranslateMessage(&Message);
        DispatchMessage(&Message);
    }
    return Message.wParam;
}

long WINAPI WndProc(HWND hWnd,UINT iMessage,WPARAM wParam,LPARAM lParam)
{
    HDC hDC;
    int x,y;
    static BOOL bCircle = FALSE,bRect = FALSE;
    PAINTSTRUCT ps;
    x = LOWORD(lParam);
    y = HIWORD(lParam);
    switch(iMessage)
    {
    case WM_MOUSEMOVE:
        rect1.right = x;
        rect1.bottom = y;
        if(bCircle == TRUE || bRect == TRUE)
        InvalidateRect(hWnd,NULL,TRUE);
        break;
    case WM_LBUTTONDOWN:
        if(wParam & MK_CONTROL)
        {
            bCircle = TRUE;
            bRect = FALSE;
            rect1.left = x;
            rect1.top = y;
        }
        else if(wParam & MK_SHIFT)
        {
            bRect = TRUE;
            bCircle = FALSE;
            rect1.left = x;
            rect1.top = y;
        }
        else
        {
            bCircle = FALSE;
            bRect = FALSE;
        }
        break;
    case WM_LBUTTONUP:
        bRect = FALSE;
        bCircle = FALSE;
        break;
    case WM_PAINT:
        hDC = BeginPaint(hWnd,&ps);
        if(bCircle == TRUE)
            Ellipse(hDC,rect1.left,rect1.top,rect1.right,rect1.bottom);
        if(bRect == TRUE)
            Rectangle(hDC,rect1.left,rect1.top,rect1.right,rect1.bottom);
        EndPaint(hWnd,&ps);
        break;
    case WM_DESTROY:
        PostQuitMessage(0);
        return 0;
    default:
        return(DefWindowProc(hWnd,iMessage,wParam,lParam));
    }
    return 0;
}

BOOL InitWindows(HINSTANCE hInstance,int nCmdShow)
{
    HWND hWnd;
    hWnd = CreateWindow("鼠标练习","鼠标显示实例程序",WS_OVERLAPPEDWINDOW,CW_USEDEFAULT,0,CW_USEDEFAULT,0,NULL,NULL,hInstance,NULL);
    if(!hWnd)
        return FALSE;
    hWndMain = hWnd;
    ShowWindow(hWnd,nCmdShow);
    UpdateWindow(hWnd);
    return TRUE;
}

BOOL InitWindowsClass(HINSTANCE hInstance)
{
    WNDCLASS WndClass;
    WndClass.cbClsExtra = 0;
    WndClass.cbWndExtra = 0;
    WndClass.hbrBackground = (HBRUSH)(GetStockObject(WHITE_BRUSH));
    WndClass.hCursor = LoadCursor(NULL,IDC_ARROW);
    WndClass.hIcon = LoadIcon(NULL,IDI_APPLICATION);
    WndClass.hInstance = hInstance;
    WndClass.lpfnWndProc = WndProc;
    WndClass.lpszClassName = "鼠标练习";
    WndClass.style = 0;
    return RegisterClass(&WndClass);
}


