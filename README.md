# listview
listview的优化_加载一种布局
   
  
     @Override
      public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder1 viewHolder1=null;
          if(convertView==null){
              //加载布局
              convertView=inflter.inflate(R.layout.list_item1, null);

              viewHolder1=new ViewHolder1();

              //找控件，把控件放入viewHolder1中
            viewHolder1.username= (EditText)convertView.findViewById(R.id.username);
            viewHolder1.age= (EditText)convertView.findViewById(R.id.age);
            viewHolder1.sex= (EditText)convertView.findViewById(R.id.sex);
            viewHolder1.icon=(ImageView)convertView.findViewById(R.id.icon);


              convertView.setTag(viewHolder1);
          }else{

              viewHolder1=(ViewHolder1)convertView.getTag();
          }

        //赋值
        viewHolder1.username.setText(list.get(position).getUsername());
        viewHolder1.age.setText(list.get(position).getAge());

        viewHolder1.sex.setText(list.get(position).getSex());
      //  viewHolder1.icon.setImageResource(list.get(position).getIcon());



        return convertView;
    }



     //代理类找控件
       class ViewHolder1{
            EditText username,age,sex;

            ImageView icon;

    }
}
