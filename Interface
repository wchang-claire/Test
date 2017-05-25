function varargout = test1(varargin)
% TEST1 MATLAB code for test1.fig
%      TEST1, by itself, creates a new TEST1 or raises the existing
%      singleton*.
%
%      H = TEST1 returns the handle to a new TEST1 or the handle to
%      the existing singleton*.
%
%      TEST1('CALLBACK',hObject,eventData,handles,...) calls the local
%      function named CALLBACK in TEST1.M with the given input arguments.
%
%      TEST1('Property','Value',...) creates a new TEST1 or raises the
%      existing singleton*.  Starting from the left, property value pairs are
%      applied to the GUI before test1_OpeningFcn gets called.  An
%      unrecognized property name or invalid value makes property application
%      stop.  All inputs are passed to test1_OpeningFcn via varargin.
%
%      *See GUI Options on GUIDE's Tools menu.  Choose "GUI allows only one
%      instance to run (singleton)".
%
% See also: GUIDE, GUIDATA, GUIHANDLES

% Edit the above text to modify the response to help test1

% Last Modified by GUIDE v2.5 24-May-2017 11:32:03

% Begin initialization code - DO NOT EDIT
gui_Singleton = 1;
gui_State = struct('gui_Name',       mfilename, ...
                   'gui_Singleton',  gui_Singleton, ...
                   'gui_OpeningFcn', @test1_OpeningFcn, ...
                   'gui_OutputFcn',  @test1_OutputFcn, ...
                   'gui_LayoutFcn',  [] , ...
                   'gui_Callback',   []);
if nargin && ischar(varargin{1})
    gui_State.gui_Callback = str2func(varargin{1});
end

if nargout
    [varargout{1:nargout}] = gui_mainfcn(gui_State, varargin{:});
else
    gui_mainfcn(gui_State, varargin{:});
end
% End initialization code - DO NOT EDIT


% --- Executes just before test1 is made visible.
function test1_OpeningFcn(hObject, eventdata, handles, varargin)
% This function has no output args, see OutputFcn.
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
% varargin   command line arguments to test1 (see VARARGIN)

% Choose default command line output for test1
handles.output = hObject;

% Update handles structure
guidata(hObject, handles);

% UIWAIT makes test1 wait for user response (see UIRESUME)
% uiwait(handles.figure1);


% --- Outputs from this function are returned to the command line.
function varargout = test1_OutputFcn(hObject, eventdata, handles) 
% varargout  cell array for returning output args (see VARARGOUT);
% hObject    handle to figure
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Get default command line output from handles structure
varargout{1} = handles.output;


% --- Executes on button press in pushbutton1.
function pushbutton1_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
% here we load the image
% im -> image loaded; im2 -> back up image (do not change)
global im im2 map H hue sat hdrG im_trans
[path,user_cance]=imgetfile();
if user_cance
    msgbox(sprintf('Error'),'Error','Error');
    return
end
[im,map]=imread(path);
im=im2double(im); %convert to double
hdrG = im; %hdr backup
im2 = hdrG; %for backup process
H = rgb2hsv(hdrG); %for hue and saturation adjustment
hue = 1; %initialization of hue
sat = 1; %initialization of sat
axes(handles.orgIm);
imshow(im);

% --- Executes on button press in pushbutton2.
function pushbutton2_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
% here we reset the image to original
global hdrG
axes(handles.newIm);
imshow(hdrG);

% --- Executes on button press in pushbutton3.
function pushbutton3_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton3 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
%this is for black and white
global hdrG im_trans
im_trans=hdrG;
im_trans=1-hdrG;
axes(handles.newIm);
imshow(im_trans);

% --- Executes on button press in pushbutton4.
function pushbutton4_Callback(hObject, eventdata, handles)
% hObject    handle to pushbutton4 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

%here we convert image to grayscal using r=g=b=(r+g+b)/3
global hdrG im_trans
im_trans=(hdrG(:,:,1)+hdrG(:,:,2)+hdrG(:,:,3))/3;
axes(handles.newIm);
imshow(im_trans);

% --- Executes on selection change in pop.
function pop_Callback(hObject, eventdata, handles)
% hObject    handle to pop (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: contents = cellstr(get(hObject,'String')) returns pop contents as cell array
%        contents{get(hObject,'Value')} returns selected item from pop

global hdrG im_trans
a = get(handles.pop,'value');
R=hdrG(:,:,1);
G=hdrG(:,:,2);
B=hdrG(:,:,3);
switch a
    case 1
    Ra=adapthisteq(R,'ClipLimit',0.02,'Distribution','uniform');
    Ga=adapthisteq(G,'ClipLimit',0.02,'Distribution','uniform');
    Ba=adapthisteq(B,'ClipLimit',0.02,'Distribution','uniform');
    case 2
    Ra=adapthisteq(R,'ClipLimit',0.02,'Distribution','exponential');
    Ga=adapthisteq(G,'ClipLimit',0.02,'Distribution','exponential');
    Ba=adapthisteq(B,'ClipLimit',0.02,'Distribution','exponential');
    case 3
    Ra=adapthisteq(R,'ClipLimit',0.02,'Distribution','rayleigh');
    Ga=adapthisteq(G,'ClipLimit',0.02,'Distribution','rayleigh');
    Ba=adapthisteq(B,'ClipLimit',0.02,'Distribution','rayleigh'); 
end
im_trans(:,:,1)=Ra;
im_trans(:,:,2)=Ga;
im_trans(:,:,3)=Ba;
%J=lab2rgb(LAB);
axes(handles.newIm);
imshow(im_trans);

% --- Executes during object creation, after setting all properties.
function pop_CreateFcn(hObject, eventdata, handles)
% hObject    handle to pop (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: popupmenu controls usually have a white background on Windows.
%       See ISPC and COMPUTER.
if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end


% --- Executes on selection change in pop2.
function pop2_Callback(hObject, eventdata, handles)
% hObject    handle to pop2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: contents = cellstr(get(hObject,'String')) returns pop2 contents as cell array
%        contents{get(hObject,'Value')} returns selected item from pop2

global hdrG im_trans
b = get(handles.pop2,'value');
im=im2double(hdrG);
R=im(:,:,1);
G=im(:,:,2);
B=im(:,:,3);
switch b
    case 1
    min = 0;
    max = 0.1;
    case 2
    min = 0;
    max = 0.2;
    case 3
    min = 0;
    max = 0.3;
    case 4
    min = 0.1;
    max = 0.4;
    case 5
    min = 0.1;
    max = 0.5;
    case 6
    min = 0.2;
    max = 0.6;
    case 7
    min = 0.3;
    max = 0.7;
    case 8
    min = 0.4;
    max = 0.8;
    case 9
    min = 0.5;
    max = 0.9;
end
im_trans(:,:,1)=imadjust(R,[min,max],[],1);
im_trans(:,:,2)=imadjust(G,[min,max],[],1);
im_trans(:,:,3)=imadjust(B,[min,max],[],1);
%J=lab2rgb(LAB);
axes(handles.newIm);
imshow(im_trans);

% --- Executes during object creation, after setting all properties.
function pop2_CreateFcn(hObject, eventdata, handles)
% hObject    handle to pop2 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: popupmenu controls usually have a white background on Windows.
%       See ISPC and COMPUTER.
if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end



function edit1_Callback(hObject, eventdata, handles)
% hObject    handle to edit1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'String') returns contents of edit1 as text
%        str2double(get(hObject,'String')) returns contents of edit1 as a double


% --- Executes during object creation, after setting all properties.
function edit1_CreateFcn(hObject, eventdata, handles)
% hObject    handle to edit1 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: edit controls usually have a white background on Windows.
%       See ISPC and COMPUTER.
if ispc && isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor','white');
end


% --- Executes on slider movement.
function slider_hue_Callback(hObject, eventdata, handles)
% hObject    handle to slider_hue (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
global H hue sat im_trans
hue=get(hObject,'Value');
H_return = cat(3,hue.*H(:,:,1),sat.*H(:,:,2),H(:,:,3));
im_trans = hsv2rgb(H_return);
axes(handles.newIm);
imshow(im_trans);

% --- Executes during object creation, after setting all properties.
function slider_hue_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider_hue (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end


% --- Executes on slider movement.
function slider_sat_Callback(hObject, eventdata, handles)
% hObject    handle to slider_sat (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
global H hue sat im_trans
sat=get(hObject,'Value');
H_return = cat(3,hue.*H(:,:,1),sat.*H(:,:,2),H(:,:,3));
im_trans= hsv2rgb(H_return);
axes(handles.newIm);
imshow(im_trans);

% --- Executes during object creation, after setting all properties.
function slider_sat_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider_sat (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end


% --- Executes on slider movement.
function slider4_Callback(hObject, eventdata, handles)
% hObject    handle to slider4 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider

% here we implement simple brightness
global hdrG im_trans
lab = rgb2lab(hdrG);
val=get(hObject,'Value');
H_return = cat(3,val*lab(:,:,1),lab(:,:,2),lab(:,:,3));
im_trans = lab2rgb(H_return);
axes(handles.newIm);
imshow(im_trans);

% --- Executes during object creation, after setting all properties.
function slider4_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider4 (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end


% --- Executes on slider movement.
function slider_map_Callback(hObject, eventdata, handles)
% hObject    handle to slider_map (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)

% Hints: get(hObject,'Value') returns position of slider
%        get(hObject,'Min') and get(hObject,'Max') to determine range of slider
% ColorMap
global hdrG im_trans
i=get(hObject,'Value');
lin1 = [0.9,0.9,0.8,0.8,0.7,0.7,0.4,0.2,0.2,0.1,0]; %if low_in of channel R is low, then R majors, otherwise, B&G matters
lin2 = [0.9,0.8,0.6,0.4,0.2, 0, 0.2,0.4,0.6,0.8,0.9]; %so if we want to creat a colormap, with colder color, we put B>G>R
lin3 = [0,0.1,0.2,0.2,0.4,0.6,0.7,0.8,0.8,0.9,0.9];
hin1 = [1,1,0.9,0.9,0.8,0.8,0.6,0.5,0.7,0.8,1];
hin2 = [1,1,0.8,0.7,0.7,1,0.8,0.6,0.7,0.9,1];
hin3 = [1,0.8,0.7,0.5,0.6,0.7,0.8,0.9,0.9,1,1];
im_trans = imadjust(hdrG,[lin1(i) lin2(i) lin3(i);hin1(i) hin2(i) hin3(i)],[]);
axes(handles.newIm);
imshow(im_trans);

% --- Executes during object creation, after setting all properties.
function slider_map_CreateFcn(hObject, eventdata, handles)
% hObject    handle to slider_map (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    empty - handles not created until after all CreateFcns called

% Hint: slider controls usually have a light gray background.
if isequal(get(hObject,'BackgroundColor'), get(0,'defaultUicontrolBackgroundColor'))
    set(hObject,'BackgroundColor',[.9 .9 .9]);
end


% --- Executes on button press in zoomin.
function zoomin_Callback(hObject, eventdata, handles)
% hObject    handle to zoomin (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global im_trans
axes(handles.newIm);
imshow(im_trans);
zoom on

% --- Executes on button press in zoomout.
function zoomout_Callback(hObject, eventdata, handles)
% hObject    handle to zoomout (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global im_trans
axes(handles.newIm);
imshow(im_trans);
zoom off


% --- Executes on button press in hdrG.
function hdrG_Callback(hObject, eventdata, handles)
% hObject    handle to hdrG (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global im hdrG
if im(1,1,1)==0.8000
    image = 1;
elseif im(1,1,1)==0
    image = 2;
end
hdrG = HDR_Global(image);
axes(handles.Global);
imshow(hdrG);

% --- Executes on button press in hdrL.
function hdrL_Callback(hObject, eventdata, handles)
% hObject    handle to hdrL (see GCBO)
% eventdata  reserved - to be defined in a future version of MATLAB
% handles    structure with handles and user data (see GUIDATA)
global im
if im(1,1,1)==0.8000
    image = 1;
elseif im(1,1,1)==0
    image = 2;
end
hdrL = HDR_Local(image);
axes(handles.Local);
imshow(hdrL);
