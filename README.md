<%@ page import="java.io.*,java.sql.*,com.dal.*" errorPage="adminlogin.jsp" %>
 
<%!
String userID="",userName="";
%>

<%
HttpSession hs=request.getSession(false);
if (hs!= null)
{
	if(!(hs.getAttribute("valid").equals("yes")))
	{
		response.sendRedirect("adminlogin.jsp");
	}
	else
	{
		userID=(String)hs.getAttribute("userID");
		userName=(String)hs.getAttribute("userName");
	}
}
else
{
	response.sendRedirect("adminlogin.jsp");
}

%>
<html>
<head><title>AD-Sense User Creation</title>
<script language="javascript">

function validate()
{
	
	var xinvalid = " "; // Invalid character is a space
    var xminLength = 6; // Minimum length
    var xpw1 = document.admincreate.c2.value;
    var xpw2 = document.admincreate.c3.value;
	var id = document.admincreate.c1.value;
	var xpassword=document.admincreate.c2.value;
    var xconfirmpassword=document.admincreate.c3.value;
	var name=document.admincreate.c4.value;
	    
	if (id == "")
    {
        window.alert("Enter User ID ");
        document.admincreate.c1.focus();
		document.admincreate.c1.select();
        return false;
    }
	else if (xpassword == "")
    {
        window.alert("Enter password");
		document.admincreate.c2.focus();
		document.admincreate.c2.select();
        return false;
    }
     else if (xconfirmpassword == "")
    {
        window.alert("Enter re-type password");
		document.admincreate.c3.focus();
        document.admincreate.c3.select();
		return false;
    }
	else if (name == "")
    {
        window.alert("Enter user name");
		document.admincreate.c4.focus();
		document.admincreate.c4.select();
        return false;
    }
    if (xpw1 == '') {
    window.alert('Enter Password');
    document.admincreate.c2.value = "";
    document.admincreate.c3.value = "";
    document.admincreate.c2.focus();
    document.admincreate.c2.select();
    return false;
   }
   else if(xpw2=='')
	{
		alert('Enter re-type password' );
		document.admincreate.c2.value = "";
        document.admincreate.c3.value = "";
		document.admincreate.c2.focus();
		document.admincreate.c2.select();
	return false;
	}
   // check for minimum length
   else if (document.admincreate.c2.value.length < xminLength)
   {
   window.alert('Password must be atleast ' + xminLength + ' characters.');
   document.admincreate.c2.value = "";
   document.admincreate.c3.value = "";
   document.admincreate.c2.focus();
   document.admincreate.c2.select();
   return false;
   }
   // check for spaces
   else if (document.admincreate.c2.value.indexOf(xinvalid) > -1)
   {
   window.alert("Spaces are not allowed");
   document.admincreate.c2.value = "";
   document.admincreate.c3.value = "";
   document.admincreate.c2.focus();
   document.admincreate.c2.select();
   return false;
   }
   else
	{
   if (xpw1 != xpw2) 
	{
   window.alert ("Password Mismatch");
   document.admincreate.c2.value = "";
   document.admincreate.c3.value = "";
   document.admincreate.c2.focus();
   document.admincreate.c2.select();
   return false;
   } 
	}

   	
     return true;
}


</script><script language="JavaScript">
 function GL_Closer() 
{
 this.close();
 window.open("signout.jsp");
}
</script>

<script language="JavaScript" >

<%
if((request.getAttribute("update"))!=null)
{
%>
	window.alert("<%=request.getAttribute("update")%>")
<%
}%>

<%
if((request.getAttribute("create"))!=null)
{
%>
	window.alert("<%=request.getAttribute("create")%>")
<%
}

%>
</script>

<style>
	a:link
 {
	color:blue;
	text-decoration:none;
	
  }

  a:visited
  {
	  color:blue;
	  text-decoration:none;
  }
  a:hover
  {
    color:blue;
	
	text-decoration:none;
  }
</style>
</head>
<body bgcolor="white" onLoad="document.admincreate.c1.focus()">

<div align="center">
  <center>
  <table border="0" width="986" height="56" bgcolor="#BD9D3C" style="border: 1 solid white">
    <tr>
      <td width="113" height="34" valign="bottom">
       </td>
      <td width="49" height="56" rowspan="2">&nbsp;</td>
      <td width="120" height="56" rowspan="2" valign="top">
        <p align="center">&nbsp;</td>
  </center>
      <td width="308" height="56" rowspan="2" valign="top">
        <p align="center"><b><font size="5" face="Lucida Calligraphy" color="#FFFFFF">AD-Sense</font></b>
		</td>
      <td width="35" height="33" valign="middle">
        <p align="right"></td>
      <td width="203" height="33" valign="top">
        <p align="right"><A HREF="adminchangepass.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b><u>Change Password</u></b></font></A></td>
      <td width="89" height="33" valign="top">
        <p align="right"><input type="button" value="Sign Out" onClick="GL_Closer()" style="background-color: #BD9D3C; color: #FFFFFF; font-family: Verdana; font-weight: bold; font-size: 10pt; text-decoration: underline; border-style: solid; border-color: #BD9D3C"></td>
    </tr>
  <center>
    <tr>
      <td width="113" height="26" valign="middle">
        </td>
      <td width="27" height="27" valign="top">
        &nbsp;</td>
  </center>
      <td width="276" height="20" colspan="2">
        <p align="right"><font face="Verdana" size="2" color="#FFFFFF"><b>Welcome&nbsp;&nbsp;&nbsp;<%=userName%></b></font></td>
    </tr>
  </table>
</div>
  <table border="1" width="985" height="23" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" bgcolor="#BD9D3C" style="background-color: #FFFFFF; color: #FFFFFF; border: 1 solid #FFFFFF">
    <tr>
      <td width="85" height="23" style="border: 1 solid #FFFFFF" bgcolor="#BD9D3C" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" align="center"><A HREF="adminhome.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b>Home</b></font></A></td>
      <td width="149" height="23" style="border: 1 solid #FFFFFF" bgcolor="#BD9D3C" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" align="center"><A HREF="adminuserdetails.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b>Admin
        Details</b></font></A></td>
      <td width="151" height="23" style="border: 1 solid #FFFFFF" bgcolor="#BD9D3C" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" align="center"><A HREF="memberdetails.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b>Member
        Details</b></font></A></td>
      <td width="154" height="23" style="border: 1 solid #FFFFFF" bgcolor="#BD9D3C" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" align="center"><A HREF="catdetails.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b>Category
        Details</b></font></A></td>
      <td width="119" height="23" style="border: 1 solid #FFFFFF" bgcolor="#BD9D3C" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" align="center"><A HREF="adsdetails.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b>Online
        Ads</b></font></A></td>
      <td width="139" height="23" style="border: 1 solid #FFFFFF" bgcolor="#BD9D3C" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" align="center"><A HREF="adsallocate.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b>Ads
        Allocation</b></font></A></td>
      <td width="142" height="23" style="border: 1 solid #FFFFFF" bgcolor="#BD9D3C" bordercolor="#FFFFFF" bordercolorlight="#FFFFFF" bordercolordark="#FFFFFF" align="center"><A HREF="memberpoints.jsp"><font face="Verdana" size="2" color="#FFFFFF"><b>Members
        Points</b></font></A></td>
    </tr>

  </table>

<form method="POST" name="admincreate" action="Admin_Create">
  <!--webbot bot="SaveResults" U-File="fpweb:///_private/form_results.txt"
  S-Format="TEXT/CSV" S-Label-Fields="TRUE" -->
<br><br>
  <div align="center">
    <table border="2" cellpadding="0" width="449" height="262" bordercolordark="#BD9D3C" bordercolor="#BD9D3C" bordercolorlight="#BD9D3C">
      <tr>
        <td width="548" height="36" valign="middle" bgcolor="#BD9D3C">
          <p align="center"><b><font face="Verdana" color="#FFFFFF" size="2">New&nbsp;
          Admin&nbsp; User</font></b></td>
      </tr>
    <center>
      <tr>
        <td width="548" height="222" valign="top">
         		    <div align="center">
            <table border="0" cellpadding="0" width="433" height="143">
              <tr>
                <td width="425" height="33" colspan="3">
               
                  <%
String status=(String)request.getAttribute("status");
System.out.println(status);
if(status==null)
{
}
else{
%>
<p align="center"><b><font face="Verdana" color="red" size="2"><%=status%></font></b></p>
<% } %>

			</td>
              </tr>
		  </center>
		      <center>
            <tr>
                <td width="217" height="44" align="right">
                <font size="2" face="Verdana"><b>User ID </b></font>

			</td>
                <td width="15" height="44" align="center">
                <font size="2" face="Verdana"><b>:</b></font>

			</td>
                <td width="193" height="44" align="left">
     <input type="text" name="c1" size="20">



			</td>
            </tr>
            <tr>
                <td width="217" height="47" align="right">
                <font size="2" face="Verdana"><b>New Password</b></font>

			</td>
                <td width="15" height="47" align="center">
                <font size="2" face="Verdana"><b>:</b></font>

			</td>
                <td width="193" height="47" align="left">
                <input type="password" name="c2" size="20">

			</td>
            </tr>
            <tr>
                <td width="217" height="39" align="right">

            <b><font face="Verdana" size="2">Re-Type New Password</font></b>

			</td>
                <td width="15" height="39" align="center">

            <b><font face="Verdana" size="2">:</font></b>

			</td>
                <td width="193" height="39" align="left">

            <input type="password" name="c3" size="20">

			</td>
            </tr>
            <tr>
                <td width="217" height="39" align="right">

            <b><font face="Verdana" size="2">User Name</font></b>

			</td>
                <td width="15" height="39" align="center">

            <b><font face="Verdana" size="2">:</font></b>

			</td>
                <td width="193" height="39" align="left">

            <input type="text" name="c4" size="20">

			</td>
            </tr>
            <tr>
                <td width="425" height="47" align="right" colspan="3">
                <p align="center"><input type="image" src="AS_Images/Create.jpg" width="63" height="25" border="0"  onClick="return validate()">

			</td>
            </tr>
            <tr>
                <td width="425" height="2" align="right" colspan="3">

			</td>
            </tr>
            </table>
          </div> 		    
       </form>

        </center>

</td>
 
    </tr>
  </table>
</div>

</body>

</html>
