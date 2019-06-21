# WGKeyboard
模仿微信的一款键盘

## 不废话直接看效果
![1.gif](https://upload-images.jianshu.io/upload_images/2404215-18c8422b9b48d162.gif?imageMogr2/auto-orient/strip)

## 使用方法
1. 引用头文件后, 直接上代码:
```objc
    UITableView *TB = [[UITableView alloc] initWithFrame:self.view.bounds];
    [self.view addSubview:TB];
    TB.dataSource = self;
    TB.delegate = self;
    
    WGKeyboard *keyboard = [WGKeyboard keyboardWithType:KeyboardTypeChat];
    [self.view addSubview:keyboard];
    _keyboard = keyboard;
    keyboard.assoTB = TB;
    keyboard.delegate = self;
    keyboard.dataSource = self;
    keyboard.recordRootPath = NSTemporaryDirectory();
    keyboard.placeholder = @"嘻嘻";
```
2. 实现对应的数据源方法:
```objc
/**
 获取表情包
 
 @param keyboard 自身
 @return 表情包
 */
- (nullable NSArray<StikerPackageModel *> *)stikerPackagesInKeyboard:(nonnull __kindof WGKeyboard *)keyboard {
    
    NSMutableArray *arrM = @[].mutableCopy;
    for (int i = 0; i < 4; i++) {
        
        StikerPackageModel *model = [StikerPackageModel new];
        [arrM addObject:model];
        
        if (i == 0) {
            
            model.stikerPackageType = StikerPackageTypeEmoji;
            model.localCover = [UIImage imageNamed:@"expression_common"];
            
            NSString *path = [[NSBundle mainBundle] pathForResource:@"emoji" ofType:@"plist"];
            NSArray *arr = [[NSArray alloc] initWithContentsOfFile:path];
            NSMutableArray<StikerInfoModel *> *emojiArrM = @[].mutableCopy;
            [arr enumerateObjectsUsingBlock:^(id  _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
                
                StikerInfoModel *stikerModel = [StikerInfoModel new];
                stikerModel.stikerType = StikerTypeEmoji;
                stikerModel.stikerTitle = obj;
                
                [emojiArrM addObject:stikerModel];
            }];
            model.stikers = emojiArrM;
        }
        else if (i == 1) {
            
            model.stikerPackageType = StikerPackageTypeColl;
            model.localCover = [UIImage imageNamed:@"expression_collect"];
            
            NSMutableArray<StikerInfoModel *> *customArrM = @[].mutableCopy;
            for (int k = 0; k < 1; k++) {
                
                if (k == 0) {
                    
                    StikerInfoModel *stikerModel = [StikerInfoModel new];
                    stikerModel.stikerType = StikerTypeAdd;
                    stikerModel.stikerTitle = @"look_add";
                    
                    [customArrM addObject:stikerModel];
                }
                else {
                    
                    StikerInfoModel *stikerModel = [StikerInfoModel new];
                    stikerModel.stikerType = StikerTypeCustom;
                    stikerModel.stikerCover = @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559805949&di=f8b76f631546bd460f75b23eeaeae14d&imgtype=jpg&er=1&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F01acc45607d5826ac7251df87e05b8.jpg%401280w_1l_2o_100sh.png";
                    stikerModel.stiker = @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559310678046&di=2b90e719e298535e22aa21c8e6415ec3&imgtype=0&src=http%3A%2F%2Fimg.mp.itc.cn%2Fq_mini%2Cc_zoom%2Cw_640%2Fupload%2F20170601%2Fc24155302f6c43e5a9c4fb26d9c3d888_th.jpg";
                    
                    [customArrM addObject:stikerModel];
                }
            }
            model.stikers = customArrM;
        }
        else if (i == 2) {
            
            model.stikerPackageType = StikerPackageTypeOffi;
            model.netCover = @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559806211&di=3d332f727fa4cf054e79c3c833cc1a37&imgtype=jpg&er=1&src=http%3A%2F%2Fimg1.cache.netease.com%2Fcatchpic%2F8%2F87%2F87BBEB021F6DE57DF0D350B6782D1F7F.JPG";
            
            NSMutableArray<StikerInfoModel *> *customArrM = @[].mutableCopy;
            for (int j = 0; j < 10; j++) {
                
                StikerInfoModel *stikerModel = [StikerInfoModel new];
                stikerModel.stikerType = StikerTypeCustom;
                stikerModel.stikerTitle = @"阿古";
                stikerModel.stikerCover = @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559728968&di=49d63ed3f7d9f518805f59cd23d6bda4&imgtype=jpg&er=1&src=http%3A%2F%2Fimg4.duitang.com%2Fuploads%2Fitem%2F201607%2F17%2F20160717061822_dJvkX.png";
                stikerModel.stiker = @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559310428842&di=c22715e59de06f31ab1f6ae0f24a59cf&imgtype=0&src=http%3A%2F%2Fimg.mp.sohu.com%2Fupload%2F20170713%2F84a1d0aec22c43f894c294a4e2de9787.png";
                
                [customArrM addObject:stikerModel];
            }
            model.stikers = customArrM;
        }
        else {
            
            model.stikerPackageType = StikerPackageTypeOffi;
            model.netCover = @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559806266&di=f266e55a4d75e34eac12eae3a4bfe6c9&imgtype=jpg&er=1&src=http%3A%2F%2Fimg.zcool.cn%2Fcommunity%2F0144d45b49b077a8012036be44456c.jpeg%40260w_195h_1c_1e_1o_100sh.jpg";
            
            NSMutableArray<StikerInfoModel *> *customArrM = @[].mutableCopy;
            for (int j = 0; j < 10; j++) {
                
                StikerInfoModel *stikerModel = [StikerInfoModel new];
                stikerModel.stikerType = StikerTypeCustom;
                stikerModel.stikerTitle = @"阿超";
                stikerModel.stikerCover = @"https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1559806330&di=7a04cde5a7b391a657863098df299586&imgtype=jpg&er=1&src=http%3A%2F%2Fi2.17173cdn.com%2F2fhnvk%2FYWxqaGBf%2Fcms3%2FoDPDPCbkBpCvpso.png";
                stikerModel.stiker = @"http://photocdn.sohu.com/20150721/mp23627612_1437451852870_2.gif";
                
                [customArrM addObject:stikerModel];
            }
            model.stikers = customArrM;
        }
    }
    return arrM;
}
```
3. 有需要的话可以实现对应的代理方法:
```objc
/**
 选择自定义表情回调
 
 @param keyboard 自身
 @param customStiker 所选自定义表情
 */
- (void)keyboard:(nonnull __kindof WGKeyboard *)keyboard didSelectCustomStiker:(nonnull StikerInfoModel *)customStiker;

/**
 点击添加表情回调
 
 @param keyboard 自身
 */
- (void)didSelectAddStikerWithKeyboard:(nonnull __kindof WGKeyboard *)keyboard;

/**
 发送按钮点击回调

 @param keyboard 自身
 @param content 内容
 */
- (void)keyboard:(nonnull __kindof WGKeyboard *)keyboard didClickSendWithContent:(nonnull NSString *)content;

/**
 录音开始回调

 @param keyboard 自身
 */
- (void)audioRecordDidStartWithKeyboard:(nonnull __kindof WGKeyboard *)keyboard;

/**
 录音完成回调
 
 @param keyboard 自身
 @param path 音频文件路径
 @param duration 时长
 */
- (void)keyboard:(nonnull __kindof WGKeyboard *)keyboard audioRecordDidFinishWithPath:(nonnull NSString *)path duration:(NSTimeInterval)duration;

/**
 录音取消回调
 
 @param keyboard 自身
 */
- (void)audioRecordDidCancelWithKeyboard:(nonnull __kindof WGKeyboard *)keyboard;

/**
 选择更多元素回调
 
 @param keyboard 自身
 @param type 更多元素类型
 */
- (void)keyboard:(nonnull __kindof WGKeyboard *)keyboard didSelectMoreItemWithType:(MoreItemType)type;

/**
 监听内容为空时删除键点击
 
 @param keyBoard 自身
 */
- (void)didDeleteBackwardWhenAvoidWithKeyBoard:(nonnull __kindof WGKeyboard *)keyBoard;
```

### 最近忙着人生大事很少回复希望大家多多见谅, 如有意见或其它想法可以多多提出, 谢谢!
