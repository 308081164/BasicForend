<template>
  <div class="app-container">

    <!--搜索表单-->
    <el-form :inline="true" :model="searchPerson" class="demo-form-inline">
      <el-form-item label="人员姓名">
        <el-input
          v-model="searchPerson.personName"
          placeholder="请输入人员姓名"
        ></el-input>
      </el-form-item>
      <el-form-item label="人员身份">
        <el-select v-model="searchPerson.personRole" placeholder="请选择">
          <el-option label="身份1" value="0"></el-option>
          <el-option label="身份2" value="1"></el-option>
          <el-option label="身份3" value="2"></el-option>
          <el-option label="身份4" value="3"></el-option>
        </el-select>
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="onSubmit">查询</el-button>
        <el-button type="info" @click="clear">清空</el-button>
      </el-form-item>
    </el-form>

    <!--按钮-->
    <el-row>
      <el-button type="danger" size="medium" @click="deleteByIds">- 批量删除</el-button>
      <el-button type="primary" size="medium" @click="dialogVisible = true; person = {};">+ 新增人员</el-button>
    </el-row>

    <!--添加数据对话框表单-->
    <el-dialog ref="form" title="编辑人员" :visible.sync="dialogVisible" width="50%">
      <el-form ref="form" :model="person" label-width="120px" size="mini">
        <el-form-item label="身份证号">
          <el-input v-model="person.id"></el-input>
        </el-form-item>

        <el-form-item label="证件类型">
          <el-select v-model="person.idType" placeholder="请选择" style="width:100%">
            <el-option label="城市" value="0"></el-option>
            <el-option label="农村" value="1"></el-option>
          </el-select>
        </el-form-item>

        <el-form-item label="姓名">
          <el-input v-model="person.name"></el-input>
        </el-form-item>
        <el-form-item label="性别">
          <el-select v-model="person.sex" placeholder="请选择" style="width:100%">
            <el-option label="男" value="0"></el-option>
            <el-option label="女" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="民族">
          <el-select v-model="person.nationality" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加民族选项 -->
            <el-option label="汉族" value="0"></el-option>
            <el-option label="其他" value="1"></el-option>
          </el-select>
        </el-form-item>
<!--        <el-form-item label="出生日期">-->
<!--          <el-date-picker v-model="person.birthday" type="date" placeholder="选择日期"></el-date-picker>-->
<!--        </el-form-item>-->
<!--        <el-form-item label="参加工作日期">-->
<!--          <el-date-picker v-model="person.workDate" type="date" placeholder="选择日期"></el-date-picker>-->
<!--        </el-form-item>-->
<!--        <el-form-item label="离退休日期">-->
<!--          <el-date-picker v-model="person.retirementDate" type="date" placeholder="选择日期"></el-date-picker>-->
<!--        </el-form-item>-->
        <el-form-item label="出生日期">
          <el-date-picker
            v-model="person.birthday"
            type="date"
            format="yyyy-MM-dd"
            placeholder="选择日期"
          ></el-date-picker>
        </el-form-item>
        <el-form-item label="参加工作日期">
          <el-date-picker
            v-model="person.workDate"
            type="date"
            format="yyyy-MM-dd"
            placeholder="选择日期"
          ></el-date-picker>
        </el-form-item>
        <el-form-item label="离退休日期">
          <el-date-picker
            v-model="person.retirementDate"
            type="date"
            format="yyyy-MM-dd"
            placeholder="选择日期"
          ></el-date-picker>
        </el-form-item>
        <el-form-item label="离退休状态">
          <el-select v-model="person.retirement" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加离退休状态选项 -->
            <el-option label="是" value="0"></el-option>
            <el-option label="否" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="户口性质">
          <el-select v-model="person.residenceType" placeholder="请选择" style="width:100%">
            <el-option label="城镇" value="0"></el-option>
            <el-option label="农村" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="户口所在地">
          <el-input v-model="person.residenceAddress"></el-input>
        </el-form-item>
        <el-form-item label="文化程度">
          <el-select v-model="person.education" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加文化程度选项 -->
            <el-option label="上过学" value="0"></el-option>
            <el-option label="没上过" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="政治面貌">
          <el-select v-model="person.politicalStatus" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加政治面貌选项 -->
            <el-option label="群众" value="0"></el-option>
            <el-option label="不是群众" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="个人身份">
          <el-select v-model="person.identity" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加个人身份选项 -->
            <el-option label="预言家" value="0"></el-option>
            <el-option label="平民" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="用工形式">
          <el-select v-model="person.employment" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加用工形式选项 -->
            <el-option label="正式工" value="0"></el-option>
            <el-option label="临时工" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="专业技术职务">
          <el-input v-model="person.technicalPosition"></el-input>
        </el-form-item>
        <el-form-item label="国家职业资格等级">
          <el-select v-model="person.workerLevel" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加职业资格等级选项 -->
            <el-option label="一级" value="0"></el-option>
            <el-option label="特级" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="婚姻状况">
          <el-select v-model="person.marriage" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加婚姻状况选项 -->
            <el-option label="单身" value="0"></el-option>
            <el-option label="丧偶" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="行政职务">
          <el-input v-model="person.administrativePosition"></el-input>
        </el-form-item>
        <el-form-item label="备注">
          <el-input v-model="person.note" type="textarea"></el-input>
        </el-form-item>
        <el-form-item label="公司">
          <el-input v-model="person.companyId"></el-input>
        </el-form-item>
        <el-form-item label="医疗人员类别">
          <el-select v-model="person.medicalPersonnel" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加医疗人员类别选项 -->
            <el-option label="类别1" value="0"></el-option>
            <el-option label="类别2" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="健康状况">
          <el-select v-model="person.health" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加健康状况选项 -->
            <el-option label="健康" value="0"></el-option>
            <el-option label="不健康" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="劳模标志">
          <el-select v-model="person.modelWorker" placeholder="请选择" style="width:100%">
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="干部标志">
          <el-select v-model="person.cadre" placeholder="请选择" style="width:100%">
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="公务员标志">
          <el-select v-model="person.civilServant" placeholder="请选择" style="width:100%">
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="在编标志">
          <el-select v-model="person.authorizedStrength" placeholder="请选择" style="width:100%">
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="居民类别">
          <el-select v-model="person.residentType" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加居民类别选项 -->
            <el-option label="常住人口" value="0"></el-option>
            <el-option label="流动人口" value="1"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="灵活就业标志">
          <el-select v-model="person.flexibleEmployment" placeholder="请选择" style="width:100%">
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="农民工标志">
          <el-select v-model="person.migrantWorker" placeholder="请选择" style="width:100%">
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="雇主标志">
          <el-select v-model="person.employer" placeholder="请选择" style="width:100%">
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="军转人员标志">
          <el-select v-model="person.militaryPersonnel" placeholder="请选择" style="width:100%">
            <!-- 需要根据实际情况添加军转人员标志选项 -->
            <el-option label="是" value="1"></el-option>
            <el-option label="否" value="0"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="社保卡号">
          <el-input v-model="person.socialSecurityId"></el-input>
        </el-form-item>
        <el-form-item label="定点医疗机构编码">
          <el-input v-model="person.medinsId"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="add">提交</el-button>
          <el-button @click="dialogVisible = false">取消</el-button>
        </el-form-item>
      </el-form>
    </el-dialog>


    <br>
    <!--表格-->
    <el-table :data="tableData" style="width: 100%" border @selection-change="handleSelectionChange">
      <el-table-column type="selection" width="55" align="center"></el-table-column>
      <el-table-column prop="peopleId" label="人员编码" align="center"></el-table-column>

      <el-table-column prop="name" label="姓名" align="center"></el-table-column>
      <el-table-column prop="id" label="身份证号" align="center"></el-table-column>
      <el-table-column prop="sex" label="性别" align="center">
        <template slot-scope="{ row }">
          <span>{{ getSexLabel(row.sex) }}</span>
        </template>
      </el-table-column>
      <el-table-column prop="birthday" label="出生日期" align="center"></el-table-column>
      <el-table-column align="center" label="操作">
        <template slot-scope="scope">
          <el-button type="primary" size="small" @click="update(scope.row.peopleId)">编辑</el-button>
          <el-button type="danger" size="small" @click="deleteById(scope.row.peopleId)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>

    <!--分页工具条-->
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :background="background"
      :current-page="currentPage"
      :page-sizes="[5, 10, 15, 20]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="totalCount">
    </el-pagination>
  </div>
</template>

<script>
import { page, add, update, deleteById, selectById } from "@/api/Person.js";

export default {
  data() {
    return {
      background: true,
      pageSize: 5,
      totalCount: 100,
      currentPage: 1,
      dialogVisible: false,
      searchPerson: {
        personName: "",
        personRole: "",
      },
      person: {
        peopleId: null,
        idType: "",
        id: "",
        name: "",
        sex: "",
        nationality: "",
        birthday: "",
        workDate: "",
        retirementDate: "",
        retirement: "",
        residenceType: "",
        residenceAddress: "",
        education: "",
        politicalStatus: "",
        identity: "",
        employment: "",
        technicalPosition: "",
        workerLevel: "",
        marriage: "",
        administrativePosition: "",
        note: "",
        companyId: null,
        medicalPersonnel: "",
        health: "",
        modelWorker: "",
        cadre: "",
        civilServant: "",
        authorizedStrength: "",
        residentType: "",
        flexibleEmployment: "",
        migrantWorker: "",
        employer: "",
        militaryPersonnel: "",
        socialSecurityId: "",
        medinsId: ""
      },
      selectedIds: [],
      multipleSelection: [],
      tableData: [],
    };
  },

  mounted() {
    this.page();
  },

  methods: {
    page() {
      page(
        this.currentPage,
        this.pageSize,
        this.searchPerson.personName,
        this.searchPerson.personRole
      ).then((res) => {
        this.totalCount = res.data.data.total;
        this.tableData = res.data.data.rows;
      });
    },

    handleSelectionChange(val) {
      this.multipleSelection = val;
    },

    onSubmit() {
      this.currentPage = 1;
      this.page();
    },

    clear() {
      this.searchPerson = { personName: "", personRole: "" };
      this.page();
    },

    add() {
      let operator;

      if (this.person.peopleId) {
        operator = update(this.person);
      } else {
        operator = add(this.person);
      }

      operator.then((resp) => {
        if (resp.data.code == "1") {
          this.dialogVisible = false;
          this.page();
          this.$message({ message: "恭喜你，保存成功", type: "success" });
          this.person = {};
        } else {
          this.$message.error(resp.data.msg);
        }
      });
    },

    update(id) {
      this.dialogVisible = true;

      selectById(id).then((result) => {
        if (result.data.code == 1) {
          this.person = result.data.data;
        }
      });
    },

    handleSizeChange(val) {
      this.pageSize = val;
      this.page();
    },

    handleCurrentChange(val) {
      this.currentPage = val;
      this.page();
    },

    deleteById(id) {
      this.$confirm("此操作将删除该数据, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      }).then(() => {
        deleteById(id).then((resp) => {
          if (resp.data.code == 1) {
            this.$message.success("恭喜你，删除成功");
            this.page();
          } else {
            this.$message.error(resp.data.msg);
          }
        });
      }).catch(() => {
        this.$message.info("已取消删除");
      });
    },

    deleteByIds() {
      this.$confirm("此操作将删除该数据, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      }).then(() => {
        this.selectedIds = this.multipleSelection.map(item => item.peopleId);

        deleteById(this.selectedIds).then((resp) => {
          if (resp.data.code == "1") {
            this.$message.success("恭喜你，删除成功");
            this.page();
          } else {
            this.$message.error(resp.data.msg);
          }
        });
      }).catch(() => {
        this.$message.info("已取消删除");
      });
    },

    getSexLabel(sex) {
      return sex === '0' ? '男' : '女';
    },
  },
};
</script>
