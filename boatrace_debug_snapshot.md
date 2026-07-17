# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-07-17T17:50:01.729517+09:00

### 次に取るべきアクション
> RED最優先: STRATEGY_CI_FAIL×17 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×31 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 STRATEGY_CI_FAIL  ×45  [2026-07-17T17:05:20]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×17  [2026-07-17T16:11:39]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×14  [2026-07-17T11:16:31]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×21  [2026-07-17T09:00:07]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=69<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=7 pred=0.1777 actual=0.5714 gap=-0.3938`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-07-17T06:00:09]
- key: `ORPHAN_SCAN|167 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift ≤-30%: n=30 hit%=33.3% ROI=0.86 (コスト 8,700/回収 7,470)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=45 hit%=33.3% ROI=0.78 (コスト 11,000/回収 8,580)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift ≥+30%: n=31 hit%=19.4% ROI=0.41 (コスト 8,700/回収 3,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=15 pred=0.2282 actual=0.2000 gap=+0.0282`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-17T06:00:09]
- key: `ROI_STAT|S00: n=176 hit%=29.0% hit_CI[Bonf]=[20.2,39.6]% ROI=0.74 ROI_boot95=[0.56,0.96]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-07-17T06:00:09]
- key: `ROI_STAT|S01_NAKAANA1: n=161 hit%=29.8% hit_CI[Bonf]=[20.6,41.0]% ROI=0.77 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-07-17T06:00:09]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=161<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-07-17T06:00:09]
- key: `ROI_STAT|S02_TETSUBAN: n=69 hit%=43.5% hit_CI[Bonf]=[27.9,60.5]% ROI=0.89 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift -10%〜+10%: n=88 hit%=31.8% ROI=0.82 (コスト 20,100/回収 16,570)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ DRIFT_BUCKET  ×1  [2026-07-17T06:00:09]
- key: `DRIFT_BUCKET|drift +10%〜+30%: n=36 hit%=30.6% ROI=0.60 (コスト 8,900/回収 5,310)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|bt=win: n=406 pred=0.4691 actual=0.3177 error=+0.1514 (+32%) brier=0.2375 [OVERC`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-07-17T06:00:09]
- key: `CALIBRATION_LIVE|S00(win): n=176 pred=0.4287 hit=0.2898 cal_err=+0.1389 brier=0.2265 BSS=-0.10 RO`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 7.84MB / last modified 2026-07-17T17:49:04.221552+09:00

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
00
2026-07-17 17:48:03,321 [INFO] predictor: Models loaded OK
2026-07-17 17:48:14,369 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=12&jcd=16&hd=20260717: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-07-17 17:48:25,902 [INFO] scraper: odds3t: 120/120 parsed
2026-07-17 17:48:27,014 [INFO] scraper: odds3f: 20/20 parsed
2026-07-17 17:48:28,161 [INFO] scraper: odds2t: 30/30 parsed
2026-07-17 17:48:28,163 [INFO] scraper: odds2f: 15/15 parsed
2026-07-17 17:48:29,267 [INFO] scraper: odds_win: 6/6 parsed
2026-07-17 17:48:29,267 [INFO] scraper: fetch_race 16/12: boats=6 odds=191/191
2026-07-17 17:48:29,270 [INFO] predictor: CALIBRATION_MODE=on
2026-07-17 17:48:29,270 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-07-17 17:48:29,274 [INFO] run_cycle: fetched 16/12 [final]: 156 combos
2026-07-17 17:48:32,672 [INFO] scraper: odds3t: 120/120 parsed
2026-07-17 17:48:33,753 [INFO] scraper: odds3f: 20/20 parsed
2026-07-17 17:48:34,828 [INFO] scraper: odds2t: 29/30 parsed
2026-07-17 17:48:34,829 [INFO] scraper: odds2f: 14/15 parsed
2026-07-17 17:48:35,897 [INFO] scraper: odds_win: 4/6 parsed
2026-07-17 17:48:35,897 [INFO] scraper: fetch_race 12/7: boats=6 odds=187/191
2026-07-17 17:48:35,900 [INFO] predictor: CALIBRATION_MODE=on
2026-07-17 17:48:35,900 [INFO] predictor: combos: {'win': 4, '2t': 29, '3t': 120}
2026-07-17 17:48:35,903 [INFO] run_cycle: fetched 12/7 [scan]: 153 combos
2026-07-17 17:48:36,004 [INFO] run_cycle: run_cycle done: 0 notifications
2026-07-17 17:49:03,767 [INFO] run_cycle: === run_cycle 17:49:03 ===
2026-07-17 17:49:03,767 [INFO] run_cycle: bet_amount_by_trust={'S': 300, 'A': 200, 'B': 100} default=100
2026-07-17 17:49:03,767 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-07-17 17:49:03,808 [INFO] predictor: Models loaded OK
2026-07-17 17:49:03,889 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 73
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 73
  }
]
```

## Phase別通知記録 (24h)
{'final': 30, 'result': 14, 'scan': 29}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 116
  FINAL_MISSING: 31
  STRATEGY_CI_FAIL: 17
  ANOMALY_SCAN_FINAL_RATIO: 2
  ANOMALY_BET_VOLUME_DROP: 1
  LARGE_ODDS_DRIFT: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 46 | 14 | 13,800 | 12,840 | -960 | 0.93 |
| S01_NAKAANA1 | 40 | 12 | 8,000 | 6,340 | -1,660 | 0.792 |
| S02_TETSUBAN | 16 | 8 | 3,200 | 4,100 | +900 | 1.281 |

## 直近アラート (24h・新しい順)
```
[17:29:43] FINAL_MISSING: {"deadline": "2026-07-17T11:57:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071716011157", "sid": "S01_NAKAANA1"}
[17:17:20] FINAL_MISSING: {"deadline": "2026-07-17T12:44:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071702051244", "sid": "S00"}
[17:12:04] FINAL_MISSING: {"deadline": "2026-07-17T16:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071701041642", "sid": "S00"}
[17:05:20] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[17:03:30] FINAL_MISSING: {"deadline": "2026-07-17T16:33:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071712041633", "sid": "S00"}
[16:58:37] FINAL_MISSING: {"deadline": "2026-07-17T12:26:00+09:00", "kind": "FINAL_MISSING", "nid": "2026071716021226", "sid": "S02_TETSUBAN"}
[16:45:04] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1057}
[16:42:37] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1086}
[16:40:21] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1081}
[16:39:25] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 1075}
```

## 本日残レース: 29件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 115件 締切済
- 通知発射: scan=26 nid / final=25 nid / result=11 nid
- predictions: 13 / うち結果DB記録済: 13
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 071R | win | 1 | 0.4989 | 2.0 | 1.00 | 200 | scan=2.2 drift=-9.1% | 15:17:19 |
| S01_NAKAANA1 | 118R | win | 1 | 0.4989 | 3.3 | 1.65 | 200 | scan=3.0 drift=+10.0% | 14:19:29 |
| S00 | 088R | win | 1 | 0.4989 | 5.4 | 2.69 | 300 | scan=6.3 drift=-14.3% | 13:55:29 |
| S01_NAKAANA1 | 117R | win | 1 | 0.4111 | 4.4 | 1.81 | 200 | scan=3.0 drift=+46.7% | 13:48:20 |
| S00 | 117R | win | 1 | 0.4111 | 4.4 | 1.81 | 300 | scan=- drift=- | 13:48:18 |
| S02_TETSUBAN | 164R | win | 1 | 0.5334 | 2.0 | 1.07 | 200 | scan=- drift=- | 13:20:19 |
| S01_NAKAANA1 | 085R | win | 1 | 0.4111 | 4.5 | 1.85 | 200 | scan=4.5 drift=+0.0% | 12:30:25 |
| S00 | 085R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=12.7 drift=-64.6% | 12:30:24 |
| S02_TETSUBAN | 135R | win | 1 | 0.5735 | 2.2 | 1.26 | 200 | scan=- drift=- | 12:27:18 |
| S00 | 024R | win | 1 | 0.2082 | 5.7 | 1.19 | 300 | scan=9.4 drift=-39.4% | 12:11:18 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 52 | +14.2% | -64.6% | +533.3% | 16 | 5 | 33 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 484.3s |
| **Latency** (scan→final max) | 610.8s |
| **Traffic** (notifications 24h) | 73 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,500円 used |
| **Saturation** (S01_NAKAANA1) | 800円 used |
| **Saturation** (S02_TETSUBAN) | 800円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| win | 407 | 0.4684 | 0.3170 | +0.1514 | 🟡+32% | 0.2374 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4273 | 0.2784 | 0.2271 | 🔴-0.13 | 0.723 |
| S01_NAKAANA1 | win | 159 | 0.4799 | 0.3019 | 0.2375 | 🔴-0.13 | 0.782 |
| S02_TETSUBAN | win | 72 | 0.5435 | 0.4444 | 0.2622 | 🔴-0.06 | 0.903 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.15-0.20 | 7 | 0.1777 | 0.5714 | 🔴-0.3938 |
| 0.20-0.30 | 15 | 0.2276 | 0.2000 | ✅+0.0276 |
| 0.30-0.50 | 156 | 0.4183 | 0.2756 | 🔴+0.1427 |
| 0.50+ | 221 | 0.5424 | 0.3529 | 🔴+0.1895 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 75 | 0.806 |
| win | <5.0 | ✅learned | 143 | 0.71 |
| win | <10.0 | ✅learned | 74 | 0.471 |
| win | <20.0 | ✅learned | 23 | 0.225 |
| win | <50.0 | ⚠️fallback | 3 | 0.1 |
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
_auto-generated by claude_snapshot.py at 2026-07-17T17:50:01.729517+09:00_