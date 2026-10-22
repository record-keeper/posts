# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-10-22T10:20:01.968981+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×50 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×18  [2026-10-22T10:02:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=84<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=175<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-10-22T06:00:13]
- key: `INSUFFICIENT_SAMPLE|S00: n=185<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1269 actual=0.3333 gap=-0.2064`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=33 pred=0.3210 actual=0.2121 gap=+0.1089`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-10-22T06:00:13]
- key: `ORPHAN_SCAN|151 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1833 actual=0.0000 gap=+0.1833`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S00: n=185 hit%=28.1% hit_CI[Bonf]=[19.7,38.4]% ROI=0.76 ROI_boot95=[0.55,0.98]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S01_NAKAANA1: n=175 hit%=36.0% hit_CI[Bonf]=[26.4,46.9]% ROI=0.98 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-10-22T06:00:13]
- key: `ROI_STAT|S02_TETSUBAN: n=84 hit%=52.4% hit_CI[Bonf]=[37.2,67.2]% ROI=0.96 ROI_boot95=[0.7`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift ≤-30%: n=29 hit%=44.8% ROI=1.16 (コスト 8,300/回収 9,630)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=47 hit%=34.0% ROI=0.72 (コスト 11,200/回収 8,120)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=92 hit%=42.4% ROI=1.19 (コスト 20,800/回収 24,780)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=63 hit%=33.3% ROI=0.86 (コスト 15,100/回収 13,040)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-10-22T06:00:13]
- key: `DRIFT_BUCKET|drift ≥+30%: n=53 hit%=24.5% ROI=0.77 (コスト 13,900/回収 10,660)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|bt=win: n=444 pred=0.4790 actual=0.3581 error=+0.1209 (+25%) brier=0.2430 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|S00(win): n=185 pred=0.4406 hit=0.2811 cal_err=+0.1595 brier=0.2371 BSS=-0.17 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|S01_NAKAANA1(win): n=175 pred=0.4931 hit=0.3600 cal_err=+0.1331 brier=0.2426 BSS`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-10-22T06:00:13]
- key: `CALIBRATION_LIVE|S02_TETSUBAN(win): n=84 pred=0.5341 hit=0.5238 cal_err=+0.0103 brier=0.2569 BSS=`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 16.38MB / last modified 2026-10-22T10:19:26.976556+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
sed
2026-10-22 10:18:18,905 [INFO] scraper: fetch_race 14/5: boats=6 odds=191/191
2026-10-22 10:18:18,908 [INFO] predictor: CALIBRATION_MODE=on
2026-10-22 10:18:18,909 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-22 10:18:18,913 [INFO] run_cycle: fetched 14/5 [final]: 156 combos
2026-10-22 10:18:19,111 [INFO] run_cycle: run_cycle done: 0 notifications
2026-10-22 10:19:03,986 [INFO] run_cycle: === run_cycle 10:19:03 ===
2026-10-22 10:19:03,986 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-10-22 10:19:03,986 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-10-22 10:19:04,015 [INFO] predictor: Models loaded OK
2026-10-22 10:19:16,485 [INFO] scraper: odds3t: 120/120 parsed
2026-10-22 10:19:17,561 [INFO] scraper: odds3f: 20/20 parsed
2026-10-22 10:19:18,638 [INFO] scraper: odds2t: 30/30 parsed
2026-10-22 10:19:18,639 [INFO] scraper: odds2f: 15/15 parsed
2026-10-22 10:19:19,714 [INFO] scraper: odds_win: 6/6 parsed
2026-10-22 10:19:19,714 [INFO] scraper: fetch_race 14/5: boats=6 odds=191/191
2026-10-22 10:19:19,717 [INFO] predictor: CALIBRATION_MODE=on
2026-10-22 10:19:19,717 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-10-22 10:19:19,721 [INFO] run_cycle: fetched 14/5 [final]: 156 combos
2026-10-22 10:19:23,342 [INFO] scraper: odds3t: 120/120 parsed
2026-10-22 10:19:24,541 [INFO] scraper: odds3f: 20/20 parsed
2026-10-22 10:19:25,653 [INFO] scraper: odds2t: 29/30 parsed
2026-10-22 10:19:25,654 [INFO] scraper: odds2f: 11/15 parsed
2026-10-22 10:19:26,726 [INFO] scraper: odds_win: 6/6 parsed
2026-10-22 10:19:26,726 [INFO] scraper: fetch_race 18/5: boats=6 odds=186/191
2026-10-22 10:19:26,728 [INFO] predictor: CALIBRATION_MODE=on
2026-10-22 10:19:26,729 [INFO] predictor: combos: {'win': 6, '2t': 29, '3t': 120}
2026-10-22 10:19:26,733 [INFO] run_cycle: fetched 18/5 [scan]: 155 combos
2026-10-22 10:19:26,846 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 56
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 56
  }
]
```

## Phase別通知記録 (24h)
{'final': 20, 'result': 15, 'scan': 21}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 89
  FINAL_MISSING: 50
  ANOMALY_SCAN_FINAL_RATIO: 18
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 43 | 14 | 12,900 | 10,980 | -1,920 | 0.851 |
| S01_NAKAANA1 | 47 | 16 | 9,400 | 7,800 | -1,600 | 0.83 |
| S02_TETSUBAN | 14 | 9 | 2,800 | 3,780 | +980 | 1.35 |

## 直近アラート (24h・新しい順)
```
[10:01:04] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[09:31:04] FINAL_MISSING: {"deadline": "2026-10-22T09:01:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102214020901", "sid": "S00"}
[09:01:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[08:00:38] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[06:00:05] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:56:03] FINAL_MISSING: {"deadline": "2026-10-21T14:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102116081421", "sid": "S00"}
[23:45:04] FINAL_MISSING: {"deadline": "2026-10-21T11:07:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102123021107", "sid": "S00"}
[23:28:03] FINAL_MISSING: {"deadline": "2026-10-21T18:55:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102112091855", "sid": "S00"}
[23:09:03] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[23:00:06] FINAL_MISSING: {"deadline": "2026-10-21T15:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026102101011526", "sid": "S00"}
```

## 本日残レース: 159件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 9件 締切済
- 通知発射: scan=1 nid / final=1 nid / result=1 nid
- predictions: 1 / うち結果DB記録済: 1
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 1件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 142R | win | 1 | 0.4111 | 3.3 | 1.36 | 200 | scan=- drift=- | 08:59:18 |
| S01_NAKAANA1 | 1211R | win | 1 | 0.5174 | 3.5 | 1.81 | 200 | scan=3.2 drift=+9.4% | 20:03:19 |
| S00 | 205R | win | 1 | 0.5334 | 8.5 | 4.53 | 300 | scan=- drift=- | 19:53:18 |
| S01_NAKAANA1 | 204R | win | 1 | 0.4111 | 3.7 | 1.52 | 200 | scan=3.5 drift=+5.7% | 19:27:44 |
| S01_NAKAANA1 | 129R | win | 1 | 0.5123 | 4.7 | 2.41 | 200 | scan=3.1 drift=+51.6% | 18:52:30 |
| S00 | 202R | win | 1 | 0.3177 | 8.4 | 2.67 | 300 | scan=10.5 drift=-20.0% | 18:31:19 |
| S01_NAKAANA1 | 128R | win | 1 | 0.4989 | 3.1 | 1.55 | 200 | scan=3.3 drift=-6.1% | 18:23:43 |
| S01_NAKAANA1 | 012R | win | 1 | 0.5990 | 3.2 | 1.92 | 200 | scan=3.0 drift=+6.7% | 15:52:30 |
| S01_NAKAANA1 | 011R | win | 1 | 0.5998 | 4.3 | 2.58 | 200 | scan=3.7 drift=+16.2% | 15:24:19 |
| S00 | 179R | win | 1 | 0.2290 | 18.7 | 4.28 | 300 | scan=14.2 drift=+31.7% | 13:56:19 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 64 | +27.8% | -42.2% | +495.8% | 10 | 3 | 39 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 490.1s |
| **Latency** (scan→final max) | 650.9s |
| **Traffic** (notifications 24h) | 56 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S01_NAKAANA1) | 200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 445 | 0.4788 | 0.3573 | +0.1215 | 🟡+25% | 0.2429 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 185 | 0.4406 | 0.2811 | 0.2371 | 🔴-0.17 | 0.757 |
| S01_NAKAANA1 | win | 176 | 0.4927 | 0.3580 | 0.2422 | 🔴-0.05 | 0.974 |
| S02_TETSUBAN | win | 84 | 0.5341 | 0.5238 | 0.2569 | 🔴-0.03 | 0.962 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.10-0.15 | 6 | 0.1269 | 0.3333 | 🔴-0.2064 |
| 0.15-0.20 | 7 | 0.1833 | 0.0000 | 🔴+0.1833 |
| 0.20-0.30 | 7 | 0.2288 | 0.2857 | 🔴-0.0570 |
| 0.30-0.50 | 158 | 0.4165 | 0.3291 | 🔴+0.0874 |
| 0.50+ | 264 | 0.5435 | 0.3864 | 🔴+0.1571 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 191 | 0.782 |
| win | <5.0 | ✅learned | 342 | 0.747 |
| win | <10.0 | ✅learned | 150 | 0.457 |
| win | <20.0 | ✅learned | 42 | 0.244 |
| win | <50.0 | ⚠️fallback | 8 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-10-22T10:20:01.968981+09:00_